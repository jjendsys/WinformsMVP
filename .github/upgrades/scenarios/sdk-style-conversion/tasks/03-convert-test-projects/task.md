# 03-convert-test-projects: Convert Test Projects

**Description**: Convert both test projects to SDK-style format with appropriate test framework support.

**Target Framework**: `net6.0-windows`

**Projects**:
1. WinFormsMvp.UnitTests
2. WinFormsMvp.PresenterFactoryUnitTests

**Scope**:
- Convert project format to SDK-style
- Migrate packages.config to PackageReference
- Migrate from MSTest to modern MSTest SDK packages
- Preserve assembly signing configuration
- Update project references

**Risk**: Low - modern MSTest SDK well-supported

**Dependencies**: Task 1 and Task 2

---

## Research Findings

### Project 1: WinFormsMvp.UnitTests
- **Path**: `WinFormsMvp.UnitTests\WinFormsMvp.UnitTests.csproj`
- **Current Target**: .NET Framework 4.6.2
- **Test Framework**: MSTest (legacy - Microsoft.VisualStudio.QualityTools.UnitTestFramework)
- **Project Type GUID**: `{3AC096D0-A1C2-E12C-1390-A8335801FDAB}` (MSTest project type)
- **Packages** (from packages.config):
  - RhinoMocks 3.6.1 (very old version from 2009)
- **Special Settings**: 
  - `SignAssembly=true`
  - References System.Windows.Forms and System.Drawing
- **Project References**: WinFormsMvp core

### Project 2: WinFormsMvp.PresenterFactoryUnitTests
- **Path**: `WinFormsMvp.PresenterFactoryUnitTests\WinFormsMvp.PresenterFactoryUnitTests.csproj`
- **Current Target**: .NET Framework 4.6.2
- **Test Framework**: MSTest (legacy)
- **Project Type GUID**: `{3AC096D0-A1C2-E12C-1390-A8335801FDAB}` (MSTest project type)
- **Packages** (from packages.config): Multiple DI container packages for testing
- **Special Settings**: `SignAssembly=true`
- **Project References**: WinFormsMvp core + all 4 DI integration projects

### Conversion Strategy

#### 1. SDK-Style Conversion
Use `convert_project_to_sdk_style` tool which will:
- Remove ProjectTypeGuids (SDK-style doesn't need them)
- Convert packages.config to PackageReference
- Simplify project file structure

#### 2. Test Framework Migration
Modern MSTest requires these packages (will be added automatically by conversion tool or manually):
- `Microsoft.NET.Test.Sdk` (test platform)
- `MSTest.TestAdapter` (MSTest runner)
- `MSTest.TestFramework` (MSTest assertions)

Remove legacy reference:
- `Microsoft.VisualStudio.QualityTools.UnitTestFramework` (obsolete)

#### 3. Target Framework Change
Change from `net462` to `net6.0-windows` since tests reference WinForms components.

#### 4. RhinoMocks Consideration
RhinoMocks 3.6.1 is very old (2009) but should still work. Will keep existing version unless build fails.

### Build Tool Selection
✓ Use `dotnet build` - modern test projects with MSTest SDK are fully supported by .NET CLI

### Expected Challenges
- May need to manually add modern MSTest packages if conversion tool doesn't detect test project type
- RhinoMocks ancient version might have compatibility issues with .NET 6
- Test discovery might need `<IsTestProject>true</IsTestProject>` property


