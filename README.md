# netcore2.1-centos7-build-issue

Captures a very simple reproduction for debugging. The issue appears where a newly created netcoreapp2.1 targeted project cannot build blaming missing assemblies (including System). Following these equivalent steps on a Windows 10 machine with .NET Core SDK 2.1 installed works flawlessly.

## Steps to reproduce

- clone this repo
- check out the branch named *master* (you are likely already here) or named *start-here* (in case master has moved)
- run the *create.sh* script
```bash
dotnet new console --name should-build --framework netcoreapp2.1
cp clean.sh ./should-build
cp fail-to-build.sh ./should-build
```
- cd into the should-build folder
- run the *clean.sh* script
```bash
rm -rf obj
rm -rf bin
```
- run the *fail-to-build.sh* script
```bash
dotnet restore
dotnet build
```
- observe the issue

Expected result : successful restore, successful build

Observed result : successful restore, failed build

```bash
> pwd
/home/jkeller/netcore2.1-centos7-build-issue/should-build
pwd
> ./clean.sh
> ./fail-to-build.sh
  Restoring packages for /home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj...
  Generating MSBuild file /home/jkeller/netcore2.1-centos7-build-issue/should-build/obj/should-build.csproj.nuget.g.props.
  Generating MSBuild file /home/jkeller/netcore2.1-centos7-build-issue/should-build/obj/should-build.csproj.nuget.g.targets.
  Restore completed in 259.17 ms for /home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj.
Microsoft (R) Build Engine version 15.7.145.53551 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 47.99 ms for /home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj.
  You are working with a preview version of the .NET Core SDK. You can define the SDK version via a global.json file in the current project. More at https://go.microsoft.com/fwlink/?linkid=869452
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(4,20): error CS0400: The type or namespace name 'System' could not be found in the global namespace (are you missing an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(10,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(11,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(12,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(13,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(14,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(15,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(16,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(4,71): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(4,99): error CS0246: The type or namespace name 'FrameworkDisplayName' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(4,122): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(10,55): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(11,61): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(12,59): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(13,68): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(14,55): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(15,53): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(16,55): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
Program.cs(1,7): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(2,7): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(3,7): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(7,7): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(8,7): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
Program.cs(5,11): error CS0518: Predefined type 'System.Object' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
Program.cs(7,26): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
Program.cs(7,16): error CS0518: Predefined type 'System.Void' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]

Build FAILED.

/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(4,20): error CS0400: The type or namespace name 'System' could not be found in the global namespace (are you missing an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(10,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(11,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(12,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(13,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(14,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(15,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(16,12): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(4,71): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(4,99): error CS0246: The type or namespace name 'FrameworkDisplayName' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(4,122): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(10,55): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(11,61): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(12,59): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(13,68): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(14,55): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(15,53): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(16,55): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
Program.cs(1,7): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(2,7): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
/tmp/.NETCoreApp,Version=v2.1.AssemblyAttributes.cs(3,7): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(7,7): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
obj/Debug/netcoreapp2.1/should-build.AssemblyInfo.cs(8,7): error CS0246: The type or namespace name 'System' could not be found (are you missing a using directive or an assembly reference?) [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
Program.cs(5,11): error CS0518: Predefined type 'System.Object' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
Program.cs(7,26): error CS0518: Predefined type 'System.String' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
Program.cs(7,16): error CS0518: Predefined type 'System.Void' is not defined or imported [/home/jkeller/netcore2.1-centos7-build-issue/should-build/should-build.csproj]
    0 Warning(s)
    26 Error(s)

Time Elapsed 00:00:01.74
```

I visited the link at [https://go.microsoft.com/fwlink/?linkid=869452](https://docs.microsoft.com/en-us/dotnet/core/tools/global-json) which indicated that *global.json* could be used to specify the tooling version used but that did not produce any changes in behavior.

This activity succeeds perfectly (using CMD equivalent steps) on a Windows 10 machine.

The issue seems like it may be related to the GitHub issues noted in the Configuration section below.

## Configuration

The filesystem seems to be XFS which is called out in GitHub issue [Directory.EnumerateDirectories doesn't return directory list on rhel7.2 #29095](https://github.com/dotnet/corefx/issues/29095) as contributing to issue [dotnet restore does not populate targets in project.assets.json on RHEL7.2 #8819](https://github.com/dotnet/cli/issues/8819). The *ftype=0*

```bash
> df
Filesystem                                     Type      Size  Used Avail Use% Mounted on
/dev/mapper/vg_sys-lv_root                     xfs       125G   63G   63G  50% /
/dev/mapper/vg_sys-lv_home                     xfs       437G  356G   81G  82% /home
```

```bash
> xfs_info /home
meta-data=/dev/mapper/vg_sys-lv_home isize=256    agcount=6, agsize=22073856 blks
         =                       sectsz=4096  attr=2, projid32bit=1
         =                       crc=0        finobt=0 spinodes=0
data     =                       bsize=4096   blocks=114509824, imaxpct=25
         =                       sunit=0      swidth=0 blks
naming   =version 2              bsize=4096   ascii-ci=0 ftype=0
log      =internal               bsize=4096   blocks=43113, version=2
         =                       sectsz=4096  sunit=1 blks, lazy-count=1
realtime =none                   extsz=4096   blocks=0, rtextents=0
```

```bash
> yum list installed | grep dotnet
dotnet-host.x86_64                    2.1.0_preview2_26411_07-1  @packages-microsoft-com-prod
dotnet-hostfxr-2.0.3.x86_64           2.0.3-1                    @packages-microsoft-com-prod
dotnet-hostfxr-2.0.5.x86_64           2.0.5-1                    @packages-microsoft-com-prod
dotnet-hostfxr-2.0.7.x86_64           2.0.7-1                    @packages-microsoft-com-prod
dotnet-hostfxr-2.1.0-preview2-26406-04.x86_64
dotnet-hosting-2.0.7.x86_64           2.0.7-1                    @packages-microsoft-com-prod
dotnet-runtime-2.0.3.x86_64           2.0.3-1                    @packages-microsoft-com-prod
dotnet-runtime-2.0.5.x86_64           2.0.5-1                    @packages-microsoft-com-prod
dotnet-runtime-2.0.7.x86_64           2.0.7-1                    @packages-microsoft-com-prod
dotnet-runtime-2.1.0-preview2-26406-04.x86_64
dotnet-runtime-deps-2.1.0-preview2-26406-04.x86_64
dotnet-sdk-2.0.3.x86_64               2.0.3-1                    @packages-microsoft-com-prod
dotnet-sdk-2.1.105.x86_64             2.1.105-1                  @packages-microsoft-com-prod
dotnet-sdk-2.1.300-preview2-008533.x86_64
dotnet-sdk-2.1.4.x86_64               2.1.4-1                    @packages-microsoft-com-prod
```

```bash
> dotnet --version
2.1.300-preview2-008533
```
