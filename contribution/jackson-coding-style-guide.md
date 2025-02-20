# Jackson Coding Style Guide

This document serves as the coding conventions for Java source code in the Jackson project.
Some parts of this document only apply to Java source code, while others apply to all source code in the project.

## Table of Contents

1. [Source Formatting](#source-formatting)
    1. [Indentation](#indentation)
    2. [Import Statements](#import-statements)
        1. [Wildcard Imports](#wildcard-imports)
        2. [Ordering](#ordering)
2. [Naming Conventions](#naming-conventions)
    1. [Field Naming](#field-naming)
    2. [Method Naming](#method-naming)
3. [Use of `final` Keyword](#use-of-final-keyword)
4. [Maximum Line Length](#maximum-line-length)
5. [Testing Conventions](#testing-conventions)
    1. [Test Class Naming](#test-class-naming)
    2. [Failing Tests](#failing-tests)

## Source Formatting

### Indentation

- **Rule**: Use spaces instead of tabs.
- **Amount**: 4 spaces per indentation level.

### Import Statements

#### Wildcard Imports

- **Usage**: Wildcards are permissible.
- **Threshold**: Employ wildcards for 5 or more imports from the same package.
- **Exceptions**: For frequently used packages like `java.util`, `java.io`, and main Jackson packages (
  e.g., `com.fasterxml.jackson.databind`), wildcards may be used for fewer imports.

#### Ordering

Import statements should be grouped and ordered in the following manner:

1. **JDK Imports**: Begin with standard Java (JDK) imports.
2. **General 3rd Party Imports**: Follow with imports from third-party libraries (e.g., JUnit).
3. **Jackson Core Types**: Next, import Jackson core types, in the order of annotations, core, and databind.
4. **Component-Specific Types**: For non-core Jackson components, import component-specific types last.

```java
import java.io.*;           // JDK imports
import java.util.*;

import org.junit.*;         // General 3rd party imports

import com.fasterxml.jackson.annotation.*;  // Jackson core types: annotations

import com.fasterxml.jackson.core.*;        // Jackson core types: core
import com.fasterxml.jackson.databind.*;    // Jackson core types: databind

import com.fasterxml.jackson.other.modules.*; // and some Component-specific imports (if any)

// same mechanism for static imports

...static import statements...
```

## Naming Conventions

### Field Naming

- **Non-Public Fields**: Prefix non-public member fields with an underscore (e.g., `_fieldName`).

### Method Naming

- **Public Methods**: Adhere to standard Java naming conventions.
- **Internal Methods**: Prefix methods used within the class with an underscore.
- **Sub-Class Methods**: Optionally, use a leading underscore for methods intended for subclass use, but not for
  external class calls.

## Use of `final` keyword

- **Fields**: Strongly encourage the use of `final` for fields, assigning them in the constructor to promote
  immutability.
- **Method Parameters**: Allowed but not necessarily encouraged.
- **Local Variables**: Encouraged where applicable.

## Maximum Line Length

- **Recommendation**: Lines should not exceed 100 characters.
- **Javadocs**: Strict adherence to a maximum of 100 characters per line is recommended.

## Testing Conventions

### Test Class Naming

- **XxxxTest**: Now The preferred naming convention has shifted to "XxxTest". In the past, test classes were typically
  named "TestXxx".
- **JUnit and Maven Compatibility**: It is important to note that for `JUnit` integration with `Maven`, test classes
  must
  either start or end with `"Test"` to be automatically included in test runs.

### Failing Tests

- **Dedicated Directory for Failing Tests**: For reproduction of bugs, Jackson projects keep a set of failing tests
  under `src/test/java/**/failing`.
- **Execution Policy**: These tests are excluded from automatic execution. They are specifically designed for manual
  runs to facilitate the reproduction and investigation of reported issues.