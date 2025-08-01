# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

For coding guidelines, see [GUIDELINES.md](GUIDELINES.md):

## About This Repository

This is **fflib-apex-common**, a foundational library implementing Apex Enterprise Patterns for Salesforce development. It provides base classes and utilities for:

- **Domain Layer**: Business logic encapsulation (`fflib_SObjectDomain`)
- **Selector Layer**: Data access abstraction (`fflib_SObjectSelector`)
- **Unit of Work**: Transaction management (`fflib_SObjectUnitOfWork`)
- **Service Layer**: Application service factories (`fflib_Application`)
- **Security**: Field-level and object security utilities (`fflib_SecurityUtils`)
- **Query Building**: Dynamic SOQL construction (`fflib_QueryFactory`)

## Project Structure

```
sfdx-source/apex-common/
├── main/classes/           # Core library classes
│   ├── fflib_Application.cls          # Application factories
│   ├── fflib_SObjectDomain.cls        # Domain layer base
│   ├── fflib_SObjectSelector.cls      # Selector layer base
│   ├── fflib_SObjectUnitOfWork.cls    # Unit of Work pattern
│   ├── fflib_QueryFactory.cls         # Query builder
│   ├── fflib_SecurityUtils.cls        # Security utilities
│   └── [other core classes]
└── test/classes/           # Test classes
    ├── fflib_ApplicationTest.cls
    ├── fflib_SObjectDomainTest.cls
    └── [other test classes]
```

## Essential Commands

### Salesforce CLI Operations

1. **Create scratch org**: `sf org create scratch --definition-file config/project-scratch-def.json --set-default --duration-days 1`
2. **Deploy fflib-apex-mocks dependency**:
   ```bash
   git clone https://github.com/apex-enterprise-patterns/fflib-apex-mocks.git temp/fflib-apex-mocks
   cd temp/fflib-apex-mocks
   sf project deploy start --ignore-conflicts
   cd ../..
   ```
3. **Deploy this library**: `sf project deploy start`
4. **Run tests**: `sf apex run test --wait 5`

**CRITICAL**: You MUST deploy fflib-apex-mocks BEFORE deploying this library. This library depends on ApexMocks and will fail to compile without it.

## Key Architecture Concepts

### Application Factory Pattern

`fflib_Application` provides factory classes for:

- `UnitOfWorkFactory` - Creates Unit of Work instances
- `SelectorFactory` - Creates Selector instances
- `ServiceFactory` - Creates Service layer instances
- `DomainFactory` - Creates Domain instances

### Security Mode Support

As of December 2022, the library supports native Apex User Mode:

- Use `dataAccess` constructor parameters instead of deprecated `enforceCRUD`/`enforceFLS` flags
- `fflib_SObjectUnitOfWork.UserModeDML` supports explicit `USER_MODE`/`SYSTEM_MODE`
- Performance benefits and clearer security behavior than `with sharing` declarations

### Selector Pattern

`fflib_SObjectSelector` provides:

- Consistent SOQL query construction
- Field-level security enforcement
- Standard field selection methods
- Integration with `fflib_QueryFactory` for complex queries

### Domain Pattern

`fflib_SObjectDomain` enables:

- Business logic encapsulation by SObject type
- Trigger handling with consistent patterns
- Validation logic centralization
- Integration with Unit of Work for DML operations

## Testing Approach

- All core classes have corresponding test classes in `test/classes/`
- Tests use ApexMocks framework for mocking dependencies
- GitHub Actions runs full test suite on every push/PR
- Sample code project tests are also executed to verify integration

## File Naming Conventions

- All library classes prefixed with `fflib_`
- Interfaces prefixed with `fflib_I` (e.g., `fflib_ISObjectDomain`)
- Test classes suffixed with `Test` (e.g., `fflib_ApplicationTest`)
- Metadata files use `-meta.xml` suffix
