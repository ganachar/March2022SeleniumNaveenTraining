# March2022 Selenium OpenCart Automation

This repository is a Java + Selenium + TestNG automation framework for the OpenCart demo app.

## General structure

- `src/main/java/com/qa/opencart/pages`: Page Object Model classes (`LoginPage`, `AccountsPage`, `SearchResultsPage`, `ProductInfoPage`, `RegisterPage`).
- `src/main/java/com/qa/opencart/factory`: Driver and browser setup (`DriverFactory`, `OptionsManager`).
- `src/main/java/com/qa/opencart/utils`: Reusable helpers (`ElementUtil` for actions/waits, `ExcelUtil` for data-driven tests).
- `src/main/java/com/qa/opencart/listeners`: Reporting/retry listeners for TestNG (`ExtentReportListener`, `TestAllureListener`, `AnnotationTransformer`, `Retry`).
- `src/main/java/com/qa/opencart/constants`: Shared constants (`Constants`).
- `src/test/java/com/qa/opencart/base`: Test bootstrap (`BaseTest`) for setup/teardown and page object initialization.
- `src/test/java/com/qa/opencart/tests`: Test classes (`LoginPageTest`, `AccountsPageTest`, `RegisterTest`).
- `src/test/resources/config`: Environment config files (`qa`, `stage`, `dev`, `uat`, `prod`).
- `src/test/resources/testrunners`: TestNG suite XML files.
- `src/test/resources/testdata`: Excel test data workbook for data providers.

## How it runs

1. `BaseTest` calls `DriverFactory` to load properties and initialize a thread-local WebDriver.
2. Driver opens the target URL and page objects are used from tests.
3. Tests are run by TestNG via Maven Surefire using `testng_regression.xml`.
4. Listeners handle retries, Extent report output, and Allure attachments.

## Important things to know

- Browser + URL + credentials + run mode (`headless`, `incognito`) are controlled via `*.config.properties`.
- Environment selection is controlled by `-Denv=<name>` (`qa` is default if omitted).
- Utility methods in `ElementUtil` are the framework's primary abstraction for Selenium interactions and waits.
- Some tests in `AccountsPageTest` are intentionally `enabled = false` and can be enabled as needed.

## Suggested learning path for newcomers

1. Read `BaseTest` and `DriverFactory` first to understand setup lifecycle.
2. Read `LoginPage` and `LoginPageTest` to understand the page-object/testing pattern used here.
3. Read `AccountsPageTest` to learn data providers, soft assertions, and end-to-end flow composition.
4. Explore listeners to understand retry/reporting and how diagnostics are captured.
5. Try adding one new page action and one matching test using existing `ElementUtil` patterns.

## Common commands

```bash
mvn test
mvn test -Denv=stage
```

