# A Packer Primer

From [Reverse Engineering Malware](http://opensecuritytraining.info/ReverseEngineeringMalware.html)...

## Background

- Packers were first created at a time when network bandwidth expensive
- UPX was a cheap way to obscure identifiable strings form Anti-Virus
- As an added bonus, it increases the complexity of analysis
- Packers progressed to Executable Protectors which use additional Anti-Analysis tricks

## Packing Process

- Packers parse the executable's headers
- Code and data is compressed/encrypted/encoded at a block level (e.g. PE section, function, string)
- A new executable is created with the encoded data and modified headers
- An unpacking program (stub) is inserted into the new file and the Entry Point points to it

## The Unpacking Stub

- The code and data is decoded
- Executable loader functions generally performed by the OS are emulated
  - Import functions are resolved assuming the packer encoded them
- Execution is transferred to the original applications code, commonly called the ''tail transition''</pre>
