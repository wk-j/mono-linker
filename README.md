## Mono Linker

-  https://www.hanselman.com/blog/ExperimentalReducingTheSizeOfNETCoreApplicationsWithMonosLinker.aspx

### Instructions

```bash
# create project
dotnet new console --language C# --output Source/MonoLinker

# add linker
dotnet add Source/MonoLinker/MonoLinker.csproj package ILLink.Tasks -v 0.1.4-preview-906439 

# publish
dotnet publish -c release -r osx.10.12-x64 -o ../../Dist/NotLinked /p:LinkDuringPublish=false Source/MonoLinker
dotnet publish -c release -r osx.10.12-x64 -o ../../Dist/Linked   Source/MonoLinker

# test size
du -m ./Dist/NotLinked
du -m ./Dist/Linked

# test function
./Dist/NotLinked/MonoLinker
./Dist/Linked/MonoLinker
```

### NuGet.config

```xml
<?xml version="1.0" encoding="utf-8"?>
<configuration>
 <packageSources>
    <add key="dotnet-core" value="https://dotnet.myget.org/F/dotnet-core/api/v3/index.json" />
 </packageSources>
</configuration>
```