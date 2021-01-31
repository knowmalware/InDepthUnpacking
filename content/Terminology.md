# Terminology

Past attempts have been made to classify malware anti-analysis techniques ([Ferrie2008](References.md),[Albertini2010](References.md),[Farley2015](References.md)).

One way of categorizing is by the analysis technique that is being attacked:

- Anti-static
- Anti-sandbox
- Anti-emulation
- Anti-debug
- Anti-dump

Another categorization is based on types of transformation:

- Obfuscation
- Packing and encoding
- Virtualization
- Self-modification

Other terms you will see in blog posts and papers on malware anti-analysis include:

- **compressor**: sole purpose is to reduce the size of the code on-disk and improve transfer speed.  Typically trivial to unpack.
- **protector**: employs any of the anti-analysis techniques
- **crypter**: uses an encryption algorithm to transform the packed binary back into code.  The algorithm may be as simple as single-byte XOR or as complex as modified variations of well-known algorithms such as Rijndael/AES.
- **bundler** / **binder** / **joiner**: a program that bundles multiple files together into a single executable that, when run, drops the files [into specific locations] and opens one or more of them.  Simplest examples are self-extracting (SFX) ZIPs and RARs.
- **dropper**: what is produced by a binder
- **downloader**: instead of containing the files that will be dropped on the system, downloads the actual malicious file(s) from one or more (often obfuscated) URLs.
- **RAT**: remote administration/access tool
- **trojan** / **troyano**: another name for a RAT
