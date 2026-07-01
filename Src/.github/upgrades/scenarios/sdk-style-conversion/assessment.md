# Assessment: SDK-style Conversion to .NET Standard 2.0

## Executive Summary
The WinFormsMVP solution contains 7 legacy-format projects targeting .NET Framework 4.6.2. All projects need conversion to SDK-style format and retargeting to .NET Standard 2.0. The main library is a WinForms MVP framework, with 5 DI container integration projects and 2 test projects.

## Projects to Convert

| Project | Path | packages.config | Type | Special Considerations | Risk |
|---------|------|-----------------|------|----------------------|------|
| WinFormsMvp | WinFormsMvp/WinFormsMvp.csproj | No | Core library | WinForms dependencies (System.Windows.Forms, System.Drawing) - needs `net*-windows` or compatibility shim | Medium |
| WinFormsMvp.UnitTests | WinFormsMvp.UnitTests/WinFormsMvp.UnitTests.csproj | Yes | Test library | MSTest, Rhino.Mocks, assembly signing | Low |
| WinFormsMvp.PresenterFactoryUnitTests | WinFormsMvp.PresenterFactoryUnitTests/WinFormsMvp.PresenterFactoryUnitTests.csproj | Yes | Test library | MSTest, DI container tests | Low |
| WinFormsMvp.Unity | WinFormsMvp.Unity/WinFormsMvp.Unity.csproj | Yes | DI integration | Unity 5.11.10, CommonServiceLocator | Low |
| WinFormsMvp.Ninject | WinFormsMvp.Ninject/WinFormsMvp.Ninject.csproj | Yes | DI integration | Ninject package | Low |
| WinFormsMvp.SimpleInjector | WinFormsMvp.SimpleInjector/WinFormsMvp.SimpleInjector.csproj | Yes | DI integration | SimpleInjector package | Low |
| WinFormsMvp.StructureMap | WinFormsMvp.StructureMap/WinFormsMvp.StructureMap.csproj | Yes | DI integration | StructureMap package | Low |

## Already SDK-style
None - all 7 projects require conversion.

## Baseline
- **Solution builds**: Yes ✓
- **Warning count**: 0
- **Test projects**: 2 (MSTest)
- **Package restore method**: packages.config (6 projects)

## Key Findings

### WinForms Compatibility Challenge
The core WinFormsMvp library references `System.Windows.Forms` and `System.Drawing`, which are **not available in .NET Standard 2.0**. Options:

1. **Target `netstandard2.0` only for DI adapters and tests**: Convert WinFormsMvp core to `net462;netcoreapp3.1;net6.0-windows` (multi-target) and keep .NET Standard 2.0 for the DI integration projects
2. **Use `net6.0-windows` or `net8.0-windows`**: Fully modernize to modern .NET with Windows Desktop support
3. **Keep `net462` for WinForms**: Only convert project format to SDK-style without changing TFM for the core library

**Recommended Approach**: Since you specifically requested .NET Standard 2.0, I'll use a hybrid approach:
- **WinFormsMvp (core)**: Multi-target `net462;net6.0-windows` to support both legacy and modern .NET
- **DI integration projects**: Target `netstandard2.0` (they don't use WinForms APIs directly)
- **Test projects**: Target `net6.0-windows` (or `net462` if tests rely on legacy behavior)

### Package Migration
6 projects use `packages.config` - all will be migrated to `PackageReference` during SDK-style conversion.

### Assembly Signing
WinFormsMvp.UnitTests has `<SignAssembly>true</SignAssembly>` - this setting will be preserved in SDK-style project.

### Custom Build Logic
No custom MSBuild targets or unusual imports detected in preliminary scan.

## Conversion Order (Topological)
1. **WinFormsMvp** (core library - no dependencies)
2. **DI Integration Projects** (depend on core):
   - WinFormsMvp.Unity
   - WinFormsMvp.Ninject
   - WinFormsMvp.SimpleInjector
   - WinFormsMvp.StructureMap
3. **Test Projects** (depend on core and DI projects):
   - WinFormsMvp.UnitTests
   - WinFormsMvp.PresenterFactoryUnitTests

## Risk Assessment
- **Overall Risk**: Medium
- **Main Risk**: WinForms APIs not available in .NET Standard 2.0
- **Mitigation**: Multi-targeting strategy for core library
- **Test Coverage**: 2 test projects available for validation
