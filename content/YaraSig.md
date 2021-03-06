# Yara: HowTo Sig

## How do I write a useful signature?

For any type of signature, whether it be Yara, Snort, Bro, or something else, **useful** means three things:

1. Low false positive and false negative rates given the expected usage of the rule
2. Efficient
   - low impact on production systems
   - ex: regex's are often processor intensive, so non-regex tests should be done first to make your rule more efficient
3. Easy to understand rule dependencies
   - snort/yara/bro version required
   - preprocessors/modules/plugins required
   - other external dependencies

Possible uses:

- Malware detection
  - across an enterprise's systems (or subset there-of)
    - filesystem
    - memory
  - incoming e-mail
  -  network traffic in general
  - [in cuckoo sandbox results](http://yara.readthedocs.org/en/latest/modules/cuckoo.html)
- Capability detection
- Classification or clustering
  - ex: I know this is malware, what kind is it?
  - generally looser constraints

## Testing

Use a test corpus to estimate the false positive and false negative rate.  For example:

- files from an Ubuntu/RedHat/Suse Linux install
  - with third-party software installed
- files from a Windows 7/8/10/Server install
  - with third-party software installed (ex: Adobe Reader, Chrome, Firefox, WinPCAP, files from www.oldapps.com)
- files from an OS X install
  - with third-party software installed (ex: Firefox, Chrome, MacPorts, Homebrew)
- memory dumps from the above
- pcap from a week's worth of traffic on a live link with systems and users representative of the network on which the rules will be deployed
- known malware, both packed and unpacked

## Low hanging fruit

For [PE files](http://yara.readthedocs.org/en/latest/modules/pe.html):

- compile timestamp
- imphash
- unique section names
- section hashes
- fuzzy hashes
  - ssdeep
  - sdhash
- parts of authenticode signatures
- unique strings (ascii, widechar, or both)

## Inverse Matching

Sometimes adversaries replace valid system files with malicious content for persistence, privilege escalation, or remote access. ([Roth2014](References.md))

Use [external variables](http://yara.readthedocs.org/en/latest/writingrules.html#external-variables) to pass the filename to the rule and match on expected aspects (ex: strings) of the knowngood file.  But be sure to [[make note|Yara]] of your use of external variables if you intend on sharing them!

## Function-based signatures

Malware and packer authors sometimes favour a particular algorithm.  For example, a string or code obfuscation technique.  If you can find such a function or basic block, then try using that as a signature.

The simplest way is to use [hexadecimal strings](http://yara.readthedocs.org/en/latest/writingrules.html#hexadecimal-strings) and copy the bytes of the function or basic block byte-for-byte.  However, if the non-local references are relocated across recompiles, then those variants will not be caught by your rule.

A more effective, though more complex and thus difficult, technique is to use hexadecimal strings but with fuzzy matching.  This requires understanding the relationship between assembly mnemonics and the binary opcodes they represent.  The best reference for this is the instruction set reference for your given architecture (ex: [Intel 64 and IA-32](http://www.intel.com/content/www/us/en/processors/architectures-software-developer-manuals.html).

To address the example above where non-local references are relocated, you can use a similar technique to [Position Independent Code (PIC) hashing](https://insights.sei.cmu.edu/sei_blog/2012/11/writing-effective-yara-signatures-to-identify-malware.html) where memory positions are ignored.  Do this by using [wild-cards and jumps](http://yara.readthedocs.org/en/latest/writingrules.html#hexadecimal-strings).

For example, if we want to turn the following into a signature:

```
8A 04 1F                mov     al, [edi+ebx]
FF 05 00 30 00 10       inc     dword_10003000
04 75                   add     al, 75h
34 3F                   xor     al, 3Fh
2C 75                   sub     al, 75h
88 03                   mov     [ebx], al
43                      inc     ebx
FF 4D FC                dec     [ebp+var_4]
75 E1                   jnz     short loc_10001158
```

The simplest way is to copy the bytes as-is:

```
{ 8A 04 1F FF 05 00 30 00 10 04 75 34 3F 2C 75 88 03 43 FF 4D FC 75 E1 }
```

However, if the program were recompiled and the data section or global variable relocated, then this signature would not match against it.  This signature would also not match if different registers or local variables are used.  Instead, use wild-cards and jumps to match on more scenarios.

```
{ 8A [2] FF 05 [4] 04 ?? 34 ?? 2c ?? 88 ?? 43 FF [2] 75 E1 }
```

In this example, the local variable and the ADD/XOR/SUB keys were ignored while the AL register was not.  This rule could be modified to match on other registers but would require more complexity and reading the Intel instruction set reference.

## Helpful Tools

[CMU SEI](http://www.sei.cmu.edu/) has released a tool named fn2yara that is able to create Yara signatures of all or individual functions in a PE32 file.  Source is available [on github](https://github.com/cmu-sei/pharos) and statically linked ELF (Linux) binaries are [on the CERT portal](https://portal.cert.org/web/mc-portal/pharos-static-analysis-tools).
