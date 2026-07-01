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

