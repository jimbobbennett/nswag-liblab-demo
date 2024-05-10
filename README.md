# NSwag and liblab demo

This demo shows how to integrate liblab as an MSBuild target in a .NET project. This project is an ASP.NET project that uses [NSwag](https://github.com/RicoSuter/NSwag) to generate an OpenAPI spec when the project is built, and then uses liblab to generate a C# SDK.

## How to run

1. Clone this repository
1. Open it in the provided dev container, or on a machine with .NET 8 and the [liblab CLI](https://developers.liblab.com/cli/cli-overview/) installed
1. Ensure you are logged in to liblab
1. Navigate to the `src` folder
1. Run `dotnet build`

The generated SDK will be in the `output/csharp` folder

## How it works

The `/src/NSwagSample.csproj` project has the following target defined:

```xml
<Target Name="liblab" AfterTargets="NSwag">
  <Exec WorkingDirectory="$(ProjectDir).." Command="liblab build --yes" />
</Target>
```

This runs after the `NSwag` target, which generates the OpenAPI spec. The `liblab` target then runs the `liblab build` command in the root folder, which generates the C# SDK using the `liblab.config.json` file in the root folder.
