# Axon Forge — Selenium Test Suite

Automated QA test suite for the Axon Forge web application, covering
network monitoring, form automation, and UI verification. Built with
Java, Selenium 4, TestNG, and Maven, and runs automatically via
GitHub Actions on every push.

## What this suite tests

- **AxonForgeNetworkTest** — Captures live network activity (API
  calls, status codes) using Chrome DevTools Protocol, to quickly
  separate frontend rendering issues from backend/API failures.
- **RelativeLocatorTest** — Automates the Contact form using
  Selenium 4 Relative Locators, Explicit Waits, and a Page Object
  Model (`ContactPage.java`) for maintainable locators.
- **ElementScreenshotTest** — Captures a screenshot of a single form
  field (rather than the full page) to verify specific UI elements
  render correctly.
- **ContactFormTest** — TestNG-driven, data-driven test suite that
  submits the Contact form with multiple input sets (valid data and
  edge cases like an empty optional field) and asserts successful
  submission.

## Tech stack

| Tool | Purpose |
|---|---|
| Java 21 | Language |
| Selenium 4.48 | Browser automation |
| TestNG 7.11 | Test runner, assertions, data providers |
| Apache Commons IO | File handling for screenshots |
| Maven | Dependency management and build |
| GitHub Actions | Continuous Integration |

## Running locally

**Prerequisites:** Java 21, Maven, Google Chrome installed.

1. Start the backend:
cd ../backend
uvicorn main:app --port 8000

2. Start the frontend:

cd ../frontend
npm run dev

3. Run the test suite:

cd selenium-tests
mvn test


Test results and reports are generated in `target/surefire-reports/`
and `test-output/` after each run.

## Continuous Integration

Every push to `main` triggers `.github/workflows/selenium-tests.yml`,
which:
1. Spins up a fresh Ubuntu environment
2. Installs Java, Node, and Python
3. Starts the backend and frontend
4. Runs the full Selenium/TestNG suite headlessly via Maven

Check the **Actions** tab on GitHub to see pass/fail status for any
commit.

## Project structure

selenium-tests/
├── src/test/java/
│ ├── ContactPage.java # Page Object Model for Contact form
│ ├── ContactFormTest.java # Data-driven TestNG test
│ ├── RelativeLocatorTest.java # Relative locators + explicit waits
│ └── ElementScreenshotTest.java
├── testng.xml # TestNG suite configuration
└── pom.xml # Maven dependencies and build config