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

