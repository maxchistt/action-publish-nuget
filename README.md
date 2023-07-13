# action-publish-nuget

Action to build latest release and publicate it on nuget as package with same version

## Example

1. Create API key on nuget.org and save it on GitHub in 'Secrets and variables'

1. Add to your .csproj file:

   ```xml
   <PropertyGroup>
       <TargetFramework>net7.0</TargetFramework>
       <ImplicitUsings>enable</ImplicitUsings>
       <Nullable>enable</Nullable>
       <Title>MyPackage</Title>
       <PackageId>MyPackage</PackageId>
       <Description>About</Description>
       <RepositoryUrl>https://github.com/user/repo</RepositoryUrl>
       <RepositoryType>git</RepositoryType>
       <Authors>NugetUsername</Authors>
   </PropertyGroup>
   ```

1. Create GitHub action:

   ```yml
   name: Release to NuGet

   on:
     release:
       types: [published]

   jobs:
     build:
       runs-on: ubuntu-latest
       timeout-minutes: 5
       steps:
         - name: NugetPublish
           uses: maxchistt/action-publish-nuget@v1
           with:
             NUGET_APIKEY: ${{secrets.NUGET_APIKEY}}
             working-directory: ./MyPackage
   ```

1. Publish GitHub release, named like 'v1.0.0' or '1.0.0'
