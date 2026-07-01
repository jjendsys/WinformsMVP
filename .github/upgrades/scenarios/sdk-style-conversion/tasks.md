# Tasks: SDK-style Conversion to .NET Standard 2.0

## Task Hierarchy

- [pending] **01-core-library**: Convert WinFormsMvp Core Library
- [pending] **02-di-projects**: Convert DI Integration Projects
- [pending] **03-test-projects**: Convert Test Projects
- [pending] **04-validation**: Final Validation

---

## Task Details

### 01-core-library
**Status**: pending
**Description**: Convert the core WinFormsMvp library to SDK-style with multi-targeting to support both .NET Framework and modern .NET Windows.

**Scope**:
- Convert project format to SDK-style
- Multi-target to `net462;net6.0-windows`
- Migrate framework references
- Preserve functionality

**Dependencies**: None

---

### 02-di-projects
**Status**: pending
**Description**: Convert all 4 DI container integration projects to SDK-style with .NET Standard 2.0 target.

**Scope**:
- WinFormsMvp.Unity
- WinFormsMvp.Ninject
- WinFormsMvp.SimpleInjector
- WinFormsMvp.StructureMap
- Target: `netstandard2.0`

**Dependencies**: 01-core-library

---

### 03-test-projects
**Status**: pending
**Description**: Convert both test projects to SDK-style format with modern test framework support.

**Scope**:
- WinFormsMvp.UnitTests
- WinFormsMvp.PresenterFactoryUnitTests
- Target: `net6.0-windows`

**Dependencies**: 01-core-library, 02-di-projects

---

### 04-validation
**Status**: pending
**Description**: Build entire solution and run all tests to ensure conversion success.

**Scope**:
- Full solution build
- Test execution
- Verification of all conversion goals

**Dependencies**: 01-core-library, 02-di-projects, 03-test-projects
