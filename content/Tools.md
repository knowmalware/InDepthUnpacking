# New Tools for the Toolbox

## OllyDbg v2

The latest version of the well established freeware Windows debugger.  Location of menu options has changed slightly.

Tips:

- Use colors, particularly one that highlights calls and jmps.
- Use labels (keyboard shortcut: colon).

### OllyDumpEx

A debugger plugin like OllyDump but with more features and cross-debugger (OllyDbg, ImmDbg, WinDbg, IDA Pro/Free, x64dbg).  Unlike OllyDump, does not include an import reconstructer built-in.

Tips:

- In general simply set OEP, but may need import reconstructor in addition.
- If unpacked into malloc/VirtualAlloc’ed segment, may have to check “Auto Adjust…”

### ScyllaHide

Multiple anti-anti-analysis techniques that can be grouped into user-defined profiles and easily loaded / changed.

### OllyExt

Multiple anti-anti-analysis techniques.  I have not personally used but was suggested as alternative to ScyllaHide.

## ImpRec

Well established and simple freeware import reconstructor.  This is what everyone suggests, but does not handle VirtualAlloc'ed segments perfectly.

Tips:

- Options
  - uncheck: Fix EP to OEP
    - since we already took care of that with OllyDumpEx
- IAT Infos Needed box (lower left)
  - change RVA to beginning of rebuilt IAT (find a CALL dword:xxxxxxxx to locate general area)
  - change Size to 800 (play around with this)
- click Get Imports button
- if bad results, click Clear Imports button and try changing things
- click Show Invalid button and then remove the invalid ones
  - multi-select then right-click and remove thunk(s)

## Scylla Import Reconstructor

A more recently updated import reconstructor with various options.

## Yara

Binary signature creation program being used to share and write custom malware signatures for classification or detection.
