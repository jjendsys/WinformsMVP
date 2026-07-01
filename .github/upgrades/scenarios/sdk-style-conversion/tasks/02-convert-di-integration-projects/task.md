# 02-convert-di-integration-projects: Convert DI Integration Projects

**Description**: Convert all 4 DI container integration projects to SDK-style with .NET Standard 2.0 target.

**Target Framework**: `netstandard2.0`

**Projects**:
1. WinFormsMvp.Unity
2. WinFormsMvp.Ninject
3. WinFormsMvp.SimpleInjector
4. WinFormsMvp.StructureMap

**Scope**:
- Convert project format to SDK-style
- Migrate packages.config to PackageReference
- Target netstandard2.0 (these don't directly use WinForms APIs)
- Update project references to WinFormsMvp core

**Risk**: Low - straightforward SDK-style conversion

**Dependencies**: Task 1 (WinFormsMvp core)

---

## Research Findings

### Projects Overview
All four projects follow the same pattern:
- Legacy non-SDK-style format
- Target .NET Framework 4.6.2
- Have packages.config for NuGet packages
- Reference WinFormsMvp core library
- Simple adapter pattern - no WinForms dependencies

### Project Details

#### 1. WinFormsMvp.Unity
- **Path**: `WinFormsMvp.Unity\WinFormsMvp.Unity.csproj`
- **Packages** (from packages.config):
  - CommonServiceLocator 2.0.7
  - System.Runtime.CompilerServices.Unsafe 6.1.2
  - Unity 5.11.10
- **Assembly Signing**: Yes (SignAssembly=true)
- **Project Reference**: WinFormsMvp

#### 2. WinFormsMvp.Ninject
- **Path**: `WinFormsMvp.Ninject\WinFormsMvp.Ninject.csproj`
- **Packages**: Ninject package
- **Project Reference**: WinFormsMvp

#### 3. WinFormsMvp.SimpleInjector
- **Path**: `WinFormsMvp.SimpleInjector\WinFormsMvp.SimpleInjector.csproj`
- **Packages**: SimpleInjector package
- **Project Reference**: WinFormsMvp

#### 4. WinFormsMvp.StructureMap
- **Path**: `WinFormsMvp.StructureMap\WinFormsMvp.StructureMap.csproj`
- **Packages**: StructureMap package
- **Project Reference**: WinFormsMvp

### Conversion Strategy
For each project:
1. Use `convert_project_to_sdk_style` tool for automated conversion
2. After conversion, change `TargetFramework` from `net462` to `netstandard2.0`
3. Verify packages.config was migrated to PackageReference
4. Verify project reference to WinFormsMvp is preserved
5. Build with `dotnet build` to validate
6. Delete packages.config file after successful build

### Expected Changes
- Project files will be dramatically smaller (SDK-style)
- packages.config will be converted to PackageReference elements
- Framework references will be implicit
- Project references will be preserved
- Assembly signing will be preserved where present

### Build Tool
✓ Can use `dotnet build` - these are simple class libraries targeting .NET Standard 2.0 with no special requirements


