# SharpMonoInjector4.8

SharpMonoInjector4.8 is a tool for injecting assemblies into Mono embedded applications, made compatible with the Microsoft .NET Framework 4.8. The target process usually does not require a restart before injecting an updated version of the assembly. Your unload method should destroy all allocated resources to prevent any memory leaks. Both x86 and x64 processes are supported.

## Concept

SharpMonoInjector works by dynamically generating machine code, writing it to the target process, and executing it using `CreateRemoteThread`. It calls functions within the Mono embedded API. The return value is obtained with `ReadProcessMemory`.

## Build

```bash
dotnet build SharpMonoInjector.Console
```
