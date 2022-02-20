---
title: JUnit 5 introduction
theme: simple
center: false
data-separator-notes: '^Note:'
---
<style type="text/css">
  .reveal {
   font-size: 30px;
  }
  .reveal p {
    text-align: left;
  }
  .reveal ul {
    display: block;
  }
  .reveal ol {
    display: block;
  }
</style>

# JUnit 5
## Some nice new features
### Matthias

> Code without test is not clean.

----
## Disclaimer
* tried to show differences to JUnit4
* get impression of some new stuff
* no guarantee on completeness
* guaranteed totally stupid examples :-)

----
## Sources
* [junit.org](https://junit.org/junit5/docs/current/release-notes/index.html)
* [blog.scottlogic.com](https://blog.scottlogic.com/2017/10/10/junit-5.html)
* [Baeldung](https://www.baeldung.com/parameterized-tests-junit-5)


---
## Switch from JUnit4 to JUnit5
### changed Annotations

| JUnit4 | JUnit5 |
|--------|--------|
| @Before / @After | @BeforeEach and @AfterEach |
| @BeforeClass / @AfterClass | @BeforeAll / @AfterAll |
| @Ignore | @Disabled |
| @Category | @Tag |
| @RunWith , @Rule and @ClassRule | "superseded" by @ExtendWith |

----
## Switch from JUnit4 to JUnit5
### new Annotations

| Annotation | Description |
|------------|-------------|
| @DisplayName("descriptive name") | descriptive name instead of Methodname |
| @Nested | nesting classes to structure tests |
| @RepeatedTest(count) | repeat a test (but what for) |
| @ParameterizedTest | more to come :-) |

----
## ```@ParameterizedTest```

* separation of test code and test cases
* different sources for test cases
  * ```@ValueSource```
  * ```@EmptySource``` / ```@NullSource``` / ```@NullAndEmptySource```
  * ```@EnumSource```
  * ```@CsvSource``` / ```@CsvFileSource```
  * ```@MethodSource```

----
## Interesting Stuff

### Testing exceptions
```Java
Exception assertThrows(ExceptionClass, Executable)
```

### Testing multiply asserts at once
```Java
void assertAll(Executable ...);
```

### Testing runtime
```Java
void assertTimeout(Duration, Executable);
```

---
## In more detail :-)

----
### Testing Exceptions
