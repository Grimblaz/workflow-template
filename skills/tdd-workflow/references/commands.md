# Test Commands Reference

> **Note**: Commands shown for Maven and Gradle with common plugins. Adapt for your build system.

## Unit Testing

### Maven

```bash
# Run all unit tests
mvn test

# Run specific test class
mvn test -Dtest=UserServiceTest

# Run specific test method
mvn test -Dtest=UserServiceTest#returnsUserWhenFoundById

# Run tests matching pattern
mvn test -Dtest="*Service*"
```

### Gradle

```bash
# Run all unit tests
./gradlew test

# Run specific test class
./gradlew test --tests "UserServiceTest"

# Run specific test method
./gradlew test --tests "UserServiceTest.returnsUserWhenFoundById"

# Run tests matching pattern
./gradlew test --tests "*Service*"
```

**Expected Output:**

```text
[INFO] Tests run: 45, Failures: 0, Errors: 0, Skipped: 0
[INFO] BUILD SUCCESS
```

**Time:** Typically < 30 seconds for unit tests

---

## Coverage Testing

### Maven (JaCoCo)

```bash
# Run tests with coverage
mvn test jacoco:report

# View report
# Open: target/site/jacoco/index.html
```

### Gradle (JaCoCo)

```bash
# Run tests with coverage
./gradlew test jacocoTestReport

# View report
# Open: build/reports/jacoco/test/html/index.html
```

**Target:** ≥80% line and branch coverage

---

## Mutation Testing

### Maven (PIT)

```bash
# Run mutation tests
mvn test-compile org.pitest:pitest-maven:mutationCoverage

# View report
# Open: target/pit-reports/[timestamp]/index.html
```

### Gradle (PIT)

```bash
# Run mutation tests
./gradlew pitest

# View report
# Open: build/reports/pitest/[timestamp]/index.html
```

**Time:** 5-30 minutes depending on codebase size

**Target:** ≥80% mutation score

---

## Integration Testing

### Maven

```bash
# Run integration tests (failsafe plugin)
mvn verify

# Skip unit tests, run only integration tests
mvn verify -DskipUnitTests
```

### Gradle

```bash
# Run integration tests
./gradlew integrationTest

# Or if using test sets
./gradlew test integrationTest
```

---

## Continuous Integration

### Combined Validation

```bash
# Maven: Full validation pipeline
mvn clean verify jacoco:report pitest:mutationCoverage

# Gradle: Full validation pipeline
./gradlew clean test jacocoTestReport pitest
```

### GitHub Actions Example

```yaml
- name: Run Tests
  run: mvn test

- name: Coverage Report
  run: mvn jacoco:report

- name: Mutation Testing
  run: mvn pitest:mutationCoverage
  if: github.event_name == 'pull_request'
```

---

## Quick Reference

| Task                   | Maven Command                           | Gradle Command                |
| ---------------------- | --------------------------------------- | ----------------------------- |
| Run all tests          | `mvn test`                              | `./gradlew test`              |
| Run specific test      | `mvn test -Dtest=ClassName`             | `./gradlew test --tests "C"`  |
| Coverage report        | `mvn jacoco:report`                     | `./gradlew jacocoTestReport`  |
| Mutation testing       | `mvn pitest:mutationCoverage`           | `./gradlew pitest`            |
| Integration tests      | `mvn verify`                            | `./gradlew integrationTest`   |
| Full validation        | `mvn clean verify`                      | `./gradlew clean check`       |

---

## Related

- [quality-gates.md](./quality-gates.md) - Threshold requirements
- [../workflows/validate-coverage.md](../workflows/validate-coverage.md) - Validation workflow
