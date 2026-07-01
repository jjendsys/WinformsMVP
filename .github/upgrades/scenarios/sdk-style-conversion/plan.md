# Execution Plan: SDK-style Conversion to .NET Standard 2.0

## Overview
Convert 7 legacy-format projects to SDK-style and retarget to appropriate frameworks, respecting WinForms API availability constraints.

## Tasks

### Task 1: Convert WinFormsMvp Core Library
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

### Task 2: Convert DI Integration Projects
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

### Task 3: Convert Test Projects
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

### Task 4: Final Validation
**Description**: Build entire solution and run all tests to ensure conversion success.

**Validation Steps**:
1. Clean solution
2. Restore packages
3. Build all projects (zero errors required)
4. Verify all packages.config files removed
5. Run all unit tests
6. Verify no warnings introduced

**Success Criteria**:
- Solution builds successfully
- All tests pass
- No packages.config files remain
- All projects use SDK-style format
- Target frameworks correctly applied

**Dependencies**: Task 1, 2, and 3

---

## Execution Order
1. Task 1: WinFormsMvp core (enables dependent projects)
2. Task 2: DI integration projects (can be done in parallel after Task 1)
3. Task 3: Test projects (require Tasks 1 and 2)
4. Task 4: Final validation

## Notes
- Each task will be validated with a build before proceeding
- Original project files will be completely replaced by SDK-style versions
- packages.config files will be deleted after migration to PackageReference
- Assembly signing settings will be preserved where present
