# SharpMonoInjector4.8

SharpMonoInjector4.8 is a tool for injecting assemblies into Mono-embedded applications, made compatible with the Microsoft .NET Framework 4.8. The target process usually does not have to be restarted in order to inject an updated version of the assembly. Your unload method must to destroy all of its resources (such as game objects).

SharpMonoInjector works by dynamically generating machine code, writing it to the target process and executing it using CreateRemoteThread. The code calls functions in the mono embedded API. The return value is obtained with ReadProcessMemory.

Both x86 and x64 processes are supported.
