# Prerequisites Review

## Introduction to RE

- x86 assembly and architecture
  - endianness
  - LEA
- Data structures and algorithms
- PE files
- [Generic RE Algorithm](https://github.com/knowmalware/IntroRE/blob/master/Generic_RE_Algorithm.md)

## RE of Malware

- "telling" API calls
- data decoding
- debugging
  - Step Into vs Step Over
  - Software vs hardware breakpoints
  - On-execute vs on-access breakpoints
  - DLLs

## Tools

### IDA

- common windows
- graph view(s)
- show opcodes
- **x** - cross-references 
- **g** - go to address / address in register / expression
- **Alt-t** - string search
- **Alt-b** - binary data search
- **u** - undefine selection / current location
- **p** - create procedure / function starting at current location
- **Alt-p** - edit current function (change start/end, etc.)
- **F2** - set software breakpoint
- **F9** - run / debug
- **F7** - step into
- **F8** - step over
- **Alt-m**  - create mark, with user defined label/comment
- **Ctrl-m** - goto mark, choose from user defined labels/comments

### PEiD

- Plugins -> Krypto ANALyzer (KANAL)

### CFF Explorer

- Identifier
- Section Headers
- Import Directory
- Export Directory
- Resource Editor

### OllyDbg and OllyDump
