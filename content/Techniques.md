# General Techniques

## Look for common tail transitions

From [Reverse Engineering Malware](http://opensecuritytraining.info/ReverseEngineeringMalware.html)...

- Jump immediate (ex: jmp 0401234)
  - Jumps generally take 1 byte operand, while transitions from unpackers to application code require a larger operand (e.g. 4 bytes)
  - A call could be used in place of a jump
- push / ret
  - A push followed by a return is fishy as the pushed value becomes the return address
  - The unpacker may use a constant or set a register that it jumps to
- PUSHA / PUSHAD near EntryPoint
  - Not a transition technique, but usually used for restoring registers to entry-point state
  - Look for the associated POPA / POPAD
  - Hardware Breakpoint on-access one of the saved registers on the stack
    - View ESP in dump, select one of the 4 byte aligned values, and set breakpoint (f2)


## Conditional Tracing (with OllyDbg v2)

- Menu: Trace -> Set protocol...
  - Can improve trace speed and readability of trace log
- Menu:  Trace -> Set condition...
  - EIP is outside range (ex: section hop)
  - EIP points to modified command
  - Command is... (ex: CALL ANY)
  - Command count is...
- **Don't forget** that instead of Run, you need to Menu: Trace -> Trace into/over
- View the trace log with Menu: Trace -> Open run trace


## Execute until *action*

- API (reference RE of Malware material)
- network connection
  - specific activity
  - what if connectivity check to non-malicious domain first?
