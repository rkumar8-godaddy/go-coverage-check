# 🧪 Go PR and Total Coverage Check

A GitHub Action that enforces code coverage on **only the lines changed in a pull request**, and optionally **enforces total project coverage** for Go projects. Highly configurable with support for file and directory exclusions using regex.

---

## 🚀 Features

- ✅ Enforces minimum code coverage on **changed lines only**
- ✅ Optionally enforces **total project coverage**
- ✅ Supports regex-based **file and directory exclusions**
- ✅ Allows bypassing thresholds with flexible toggles
- ✅ Designed for Go projects using `go test` and `go tool cover`

---

## 🔧 Inputs

| Name                    | Description                                                            | Required | Default    |
|-------------------------|------------------------------------------------------------------------|----------|------------|
| `go-version`            | Go version to use                                                      | ❌       | `1.20`     |
| `min-coverage`          | Minimum allowed PR coverage (%)                                        | ❌       | `80`       |
| `min-total-coverage`    | Minimum allowed total project coverage (%)                             | ❌       | `75`       |
| `exclude-files`         | Newline-separated regex patterns to exclude specific files             | ❌       | (empty)    |
| `exclude-dirs`          | Newline-separated regex patterns to exclude directories                | ❌       | (empty)    |
| `bypass-threshold`      | Set to `true` to skip PR coverage threshold enforcement                | ❌       | `false`    |
| `bypass-total-coverage` | Set to `true` to skip total project coverage enforcement               | ❌       | `false`    |

---

## 🧑‍💻 Example Usage

```yaml
name: PR Coverage

on:
  pull_request:
    paths:
      - '**/*.go'

jobs:
  coverage:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3

      - name: Run Go Coverage Check
        uses: my-org/go-pr-and-total-coverage-check@v1
        with:
          go-version: '1.21'
          min-coverage: 85
          min-total-coverage: 80
          bypass-total-coverage: false
          exclude-files: |
            .*_gen.go$
            .*_mock.go$
          exclude-dirs: |
            ^internal/generated/
            ^third_party/
