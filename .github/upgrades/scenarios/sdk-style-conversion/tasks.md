# Tasks: SDK-style Conversion to .NET Standard 2.0

## Task Hierarchy

- [completed] **01-convert-winformsmvp-core-library**: Convert WinFormsMvp Core Library
- [completed] **02-convert-di-integration-projects**: Convert DI Integration Projects
- [completed] **03-convert-test-projects**: Convert Test Projects
- [pending] **04-final-validation**: Final Validation

---

## Task Details

### 01-convert-winformsmvp-core-library
**Status**: completed
**Description**: Convert the core WinFormsMvp library to SDK-style with multi-targeting to support both .NET Framework and modern .NET Windows.

**Scope**:
- Convert project format to SDK-style
- Multi-target to `net462;net6.0-windows`
- Migrate framework references
- Preserve functionality

**Dependencies**: None

---

### 02-convert-di-integration-projects
**Status**: pending
- Migrate framework references
- Preserve functionality

**Dependencies**: None

---

### 02-convert-di-integration-projects
**Status**: completed
**Description**: Convert all 4 DI container integration projects to SDK-style with .NET Standard 2.0 target.

**Scope**:
- WinFormsMvp.Unity
- WinFormsMvp.Ninject
- WinFormsMvp.SimpleInjector
- WinFormsMvp.StructureMap
- Target: `netstandard2.0`

**Dependencies**: 01-convert-winformsmvp-core-library

---

### 03-convert-test-projects
**Status**: completed
**Description**: Convert both test projects to SDK-style format with modern test framework support.

**Scope**:
- WinFormsMvp.UnitTests
- WinFormsMvp.PresenterFactoryUnitTests
- Target: `net6.0-windows`

**Dependencies**: 01-convert-winformsmvp-core-library, 02-convert-di-integration-projects

---

### 04-final-validation
**Status**: pending
**Description**: Build entire solution and run all tests to ensure conversion success.

**Scope**:
- Full solution build
- Test execution
- Verification of all conversion goals

**Dependencies**: 01-convert-winformsmvp-core-library, 02-convert-di-integration-projects, 03-convert-test-projects
