# SharpMonoInjector4.8

SharpMonoInjector4.8 is a tool for injecting assemblies into Mono embedded applications, made compatible with the Microsoft .NET Framework 4.8. The target process usually does not require a restart before injecting an updated version of the assembly. Your unload method should destroy all allocated resources to prevent any memory leaks. Both x86 and x64 processes are supported. You can see an example implementation [here](https://github.com/winstxnhdw/rc15-hax/tree/master/rc15-hax/Scripts).

## Requirements

- Windows 10/11
- Microsoft .NET Framework 4.8

## Concept

SharpMonoInjector works by dynamically generating machine code, writing it to the target process, and executing it using `CreateRemoteThread`. It calls functions within the Mono embedded API. The return value is obtained with `ReadProcessMemory`.

## Build

```bash
dotnet build SharpMonoInjector.Console
```

## Usage

Inject

```bash
smi.exe inject -p RobocraftClient -a rc15-hax.dll -n ExampleAssembly -c Loader -m Load
```

```yaml
Usage:
smi.exe inject <options>

Required arguments:
-p      id or name of the target process
-a      path of the assembly to inject
-n      namespace in which the loader class resides
-c      name of the loader class
-m      name of the method to invoke in the loader class
```

Eject

```bash
smi.exe eject -p RobocraftClient -a 0x13D23A98 -n ExampleAssembly -c Loader -m Unload
```

```yaml
Usage:
smi.exe eject <options>

Required arguments:
-p      id or name of the target process
-a      address of the assembly to eject
-n      namespace in which the loader class resides
-c      name of the loader class
-m      name of the method to invoke in the loader class
```
