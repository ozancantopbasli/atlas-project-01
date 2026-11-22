# Software Requirements Specification

## Project
Engineering Workflow Lab

## Purpose
Analyze synthetic application logs using a Python CLI.

## Functional Requirements

### P01-FR-01: File Input
The CLI shall accept a UTF-8 log file path as an argument.

Acceptance Criteria:
- A valid UTF-8 file can be opened.
- A missing file produces a defined error.

Test ID: P01-TEST-01

### P01-FR-02: Log Level Classification
The application shall classify ERROR, WARNING, and INFO
levels case-insensitively at the beginning of a log record.

Acceptance Criteria:
- ERROR, WARNING, and INFO are recognized.
- Lowercase and uppercase levels produce identical results.
- TERROR is not classified as ERROR.
- Unrecognized levels are marked as invalid.

Test ID: P01-TEST-02

### P01-FR-03: File Error Handling
The application shall handle file and encoding errors
using predefined exit codes and clear error messages.

Acceptance Criteria:
- A valid empty file returns exit code 0.
- A missing file returns exit code 2.
- An invalid UTF-8 file returns exit code 3.
- Error messages do not expose sensitive information.

Test ID: P01-TEST-03

### P01-FR-04: Deterministic JSON Reporting
The application shall generate a deterministic JSON report.

Acceptance Criteria:
- The report contains counts, invalid_lines, and total_lines.
- Counts include ERROR, WARNING, and INFO.
- Processing identical input produces identical JSON output.
- Processing identical input produces the same exit code.
- A valid empty file produces zero counts.

Test ID: P01-TEST-04

### P01-FR-05: Invalid Line Tracking
The application shall track invalid log lines
without silently discarding them.

Acceptance Criteria:
- Unrecognized log levels are counted as invalid.
- Blank lines are counted as invalid.
- Every physical line contributes to total_lines.
- Valid counts plus invalid_lines equals total_lines.
- An empty file contains zero total and invalid lines.

Test ID: P01-TEST-05

### P01-FR-06: CLI Usage and Help
The application shall provide a documented command-line interface.

Acceptance Criteria:
- The CLI accepts a log file path as a positional argument.
- The --help option displays usage instructions.
- The --help option exits with code 0.
- Missing required arguments produce a clear usage error.
- Invalid CLI usage returns a non-zero exit code.

Test ID: P01-TEST-06

## Non-Functional Requirements

### P01-NFR-01: Performance
The application shall support reproducible performance
measurements using a 10 MB synthetic log file.

Acceptance Criteria:
- Execution time is measured and recorded.
- Memory usage is measured and recorded.
- Python version and test environment are documented.
- A performance baseline is established.
- Performance targets are defined after baseline evaluation.

Test ID: P01-TEST-NFR-01

### P01-NFR-02: Sensitive Information Protection
The application shall prevent sensitive information
from being exposed in reports and error messages.

Acceptance Criteria:
- JSON reports contain aggregate statistics only.
- Raw log contents are not included in output.
- Error messages do not reveal absolute file paths.
- Tokens, passwords, and secrets are not exposed.
- Negative tests verify that sensitive markers are not leaked.

Test ID: P01-TEST-NFR-02

### P01-NFR-03: Environment Reproducibility
The application shall support reproducible installation
and testing on Windows PowerShell with Python 3.12.

Acceptance Criteria:
- Setup instructions are documented in README.md.
- Project dependencies are explicitly documented.
- A clean virtual environment can be created.
- Tests run successfully in the documented environment.
- Installation does not require administrator privileges.

Test ID: P01-TEST-NFR-03

### P01-NFR-04: Deterministic Behavior
The application shall produce identical results
for identical inputs under the same conditions.

Acceptance Criteria:
- Identical input produces byte-identical JSON output.
- Identical input produces the same exit code.
- JSON field ordering remains consistent.
- Reports do not contain runtime-dependent timestamps.
- Repeated analysis does not modify the input file.

Test ID: P01-TEST-NFR-04

### P01-NFR-05: Automated Testability
The application shall support automated verification
of its functional and quality requirements.

Acceptance Criteria:
- Tests are implemented using pytest.
- At least 25 meaningful automated tests are provided.
- Unit, negative, and CLI scenarios are covered.
- Tests use synthetic data and require no external services.
- All tests pass before release.
- Test failures cause a non-zero test process exit code.

Test ID: P01-TEST-NFR-05

### P01-NFR-06: Maintainability
The application shall support controlled maintenance
through readable code and documented changes.

Acceptance Criteria:
- Python code follows documented style conventions.
- Ruff lint checks pass before release.
- Parsing, classification, and reporting responsibilities are identifiable.
- README documents installation and usage.
- Significant architectural decisions are recorded in ADRs.
- Changes are verified with regression tests.

Test ID: P01-TEST-NFR-06

## Scope

### In Scope
- Read local UTF-8 synthetic log files.
- Classify ERROR, WARNING, and INFO levels.
- Track invalid and total lines.
- Generate deterministic JSON reports.
- Provide CLI usage and error handling.
- Verify behavior through automated tests.

### Out of Scope
- Web interface or REST API.
- Database integration.
- Centralized log collection or SIEM functionality.
- Processing real company or confidential logs.
- Distributed processing and Kubernetes.

## Negative Scenarios

- P01-NEG-01: Missing file returns exit code 2.
- P01-NEG-02: Invalid UTF-8 returns exit code 3.
- P01-NEG-03: TERROR is counted as invalid.
- P01-NEG-04: Blank log lines are counted as invalid.
- P01-NEG-05: Missing CLI file argument produces a usage error and non-zero exit code.
