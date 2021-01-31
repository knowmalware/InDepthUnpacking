# Flavors of DLLs

## Simple

- EntryPoint (aka DllMain) and no exports
  - `BOOL WINAPI DllMain(HINSTANCE hinstDLL, DWORD fdwReason, LPVOID lpvReserved);`
- **Remember:** DllMain is *always* called on load, unload, thread-attach, and thread-detach.
- Load with OllyDbg, which will automatically detect that it is a DLL and use a stub exe (loaddll).

## Exports

1. Load with OllyDbg
2. Breakpoint on first instruction of export function
3. Menu: Debug -> Call DLL export
   - hwnd - window handle that should be used as the owner window for any windows your DLL creates
   - hinst - your DLL's instance handle
   - lpszCmdLine - ASCIIZ command line your DLL should parse
   - nCmdShow - describes how your DLL's windows should be displayed
   - reference: https://support.microsoft.com/en-us/kb/164787

## Service

- Specific exports:
  - ServiceMain (might not be named this)
  - DllInstall
  - DllRegisterServer
  - DllUnregisterServer
- If uncertain which export to run, then modify the binary:
  1. change first two bytes of EntryPoint to EB FE (reference: https://quequero.org/2011/07/carberp-reverse-engineering/)
  2. run the service
  3. find out which process has the service DLL loaded (use Process Explorer or similar tool)
  4. attach with debugger
  5. patch the bytes back to their original
- Register services with regsrv32

## Driver

- Specific exports: DriverEntry, DllInitialize, DllUnload
