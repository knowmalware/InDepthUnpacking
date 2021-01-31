# Is it packed?

## Heuristics

- Code execution starts in last section
- Suspicious section characteristics (ex: Execute, Read, and Write)
- Virtual size incorrect in PE Header (SizeOfImage)
- Incorrect SizeOfCode in PE Header
- JMP to different section near EntryPoint
- Suspicious PE section names
- IAT includes imports by ordinal
- IAT includes **LoadLibrary** and **GetProcAddress** or **GetModuleHandle**
  - Other suspicious imports: **Sleep**, **FindFirstFile**, **FindNextFile**, **MoveFile**, **GetWindowsDirectory**, **WinExec**, **DeleteFile**, **WriteFile**, **CreateFile**, **MoveFile**, **CreateProcess**, **VirtualAllocEx**
- CALL operand, where operand is very next instruction address
- High (7+) entropy on code and/or data section(s)
- Anti-analysis techniques detected by signature (ex: Yara)
- Load with your favorite disassembler/analyzer and
  - only small part of code (.code, .text, etc) section identified as functions
  - anti-analysis techniques readily visible
- Little or no readable strings

Most of the above is based on ([Szor2005, pp467-471](References.md)).

## Tools

- PEiD
- CFF-Explorer
- exeinfo
- Yara signatures
- many, many others
