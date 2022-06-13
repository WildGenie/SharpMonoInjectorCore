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
smi.exe inject -p RobocraftClient -a rc15-hax.dll -n RC15_HAX -c Loader -m Load
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
smi.exe eject -p RobocraftClient -a 0x13D23A98 -n RC15_HAX -c Loader -m Unload
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

## Submodule

If you plan package this along with your cheats, I would recommend that you add this repository as a git submodule.

```bash
mkdir submodules
git submodule add --depth 1 https://github.com/winstxnhdw/SharpMonoInjector4.8.git ./submodules
git config -f .gitmodules submodule.submodules/SharpMonoInjector4.8.shallow true
```

To update your submodule later, simply run the following.

```bash
git submodule update --init --recursive
```

## Troubleshoot

When using this application, you may run into the following warnings.

> Unable to clear the console. To fix this issue, please ensure that the output is not being redirected.

This simply means that the console's output is being redirected elsewhere. Whether this was intentional or not, this warning is safe to ignore but it does hint some underlying issues you have with your CLI that you may be interested in fixing.

> WARNING: You are running this in an unpriveleged process, which may lead to unexpected behaviour.

No idea why [wh0am15533](https://github.com/wh0am15533) added this warning as I never had an issue running the injector without privilege elevation.

> An antivirus has been detected. If you encounter an issue, it may be necessary to disable your antivirus.

Another warning by [wh0am15533](https://github.com/wh0am15533) that had zero consequences on any of my systems. I may remove these warnings altogether when I have time to test the application further.
