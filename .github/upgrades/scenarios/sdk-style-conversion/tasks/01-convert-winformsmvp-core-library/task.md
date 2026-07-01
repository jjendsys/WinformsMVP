# 01-convert-winformsmvp-core-library: Convert WinFormsMvp Core Library

**Description**: Convert the core WinFormsMvp library to SDK-style with multi-targeting to support both .NET Framework and modern .NET Windows.

**Target Frameworks**: `net462;net6.0-windows`

**Scope**:
- Convert project format to SDK-style
- Multi-target to support WinForms across framework versions
- Migrate framework references to appropriate SDK references
- Preserve all existing functionality

**Risk**: Medium - WinForms APIs require careful framework selection

**Dependencies**: None (leaf project)

---

## Research Findings

### Project Analysis
- **Project Path**: `C:\Projects\WinformsMVP\Src\WinFormsMvp\WinFormsMvp.csproj`
- **Current Target**: .NET Framework 4.6.2 (v4.6.2)
- **Project Type**: Class library (OutputType: Library)
- **Format**: Legacy non-SDK-style
- **No packages.config**: This project only uses framework references

### Key Dependencies
**Framework References**:
- System
- System.ComponentModel.DataAnnotations
- System.Core
- System.Drawing ⚠️ (WinForms-specific)
- System.Windows.Forms ⚠️ (WinForms-specific)
- System.Xml.Linq
- System.Data.DataSetExtensions
- Microsoft.CSharp
- System.Data
- System.Xml

### WinForms Components
The project contains WinForms components that require Windows Desktop support:
- `Forms\MvpForm.cs` (Form)
- `Forms\MvpForm`.cs` (Generic Form)
- `Forms\MvpUserControl.cs` (UserControl)
- `Forms\MvpUserControl`.cs` (Generic UserControl)
- Designer files for above components

### Build Tool Selection
✓ Can use `dotnet build` - project has:
- No .resx files
- No COM references
- No VSIX/T4 templates
- Standard WinForms components (supported in SDK-style)

**Note**: Multi-targeting to `net6.0-windows` will automatically provide Windows Desktop SDK support.

### Conversion Strategy
1. Use `convert_project_to_sdk_style` tool for automated conversion
2. After conversion, add multi-targeting: change `TargetFramework` to `TargetFrameworks` with value `net462;net6.0-windows`
3. Verify System.Windows.Forms and System.Drawing are available via SDK
4. Build with `dotnet build` to validate both TFMs
5. Verify no packages.config was created (none exists now)

