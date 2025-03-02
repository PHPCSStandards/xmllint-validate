# XMLLint Validate

GitHub Action to validate XML files for being well-formed and optionally validate against an XSD schema file.

## Action inputs

| Input      | Required | Type   | Notes                                                                                 |
|------------|----------|--------|---------------------------------------------------------------------------------------|
| `pattern`  | yes      | string | The file(s) to validate. The input expects a path to a single file or a glob pattern. |
| `xsd-file` | no       | string | Path to a local file containing the XSD schema to validate against.                   |
| `xsd-url`  | no       | string | URL to a remote file containing the XSD schema to validate against.                   |

> [!NOTE]
> If both an `xsd-file` and an `xsd-url` are passed, the `xsd-file` takes precedence.

## Using the action

Validating the well-formedness of a single XML file:
```yaml
jobs:
  test:
    name: "XMLLint validate"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Validate XML file
        uses: phpcsstandards/xmllint-validate@v0
        with:
          pattern: "path/to/file.xml"
```

Glob patterns are also supported:
```yaml
jobs:
  test:
    name: "XMLLint validate"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Validate XML files
        uses: phpcsstandards/xmllint-validate@v0
        with:
          pattern: "path/to/*/docs/*.xml"
```

Validating XML files against a locally available XSD schema:
```yaml
jobs:
  test:
    name: "XMLLint validate"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Validate XML file
        uses: phpcsstandards/xmllint-validate@v1
        with:
          pattern: "path/to/*/docs/*.xml"
          xsd-file: "path/to/docs.xsd"
```

Validating XML files against a remote XSD schema:
```yaml
jobs:
  test:
    name: "XMLLint validate"
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Validate XML file
        uses: phpcsstandards/xmllint-validate@v1
        with:
          pattern: "path/to/*/docs/*.xml"
          xsd-url: "https://examples.org/docs.xsd"
```


## Contributing

Contributions to this project are welcome. Clone this repository, create a new branch, make your changes, commit them and send in a pull request.

If unsure whether the changes you are proposing would be welcome, open an issue first to discuss your proposal.


## Copyright and License

The phpcsstandards/xmllint-validate GitHub Action is ©copyright PHPCSStandards and contributors and licensed for use under the terms of the MIT License (MIT).
Please see [LICENSE](LICENSE) for more information.
