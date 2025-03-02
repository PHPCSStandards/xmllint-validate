# XMLLint Validate

GitHub Action to validate XML files for being well-formed.

## Action inputs

| Input     | Required | Type   | Notes                                                                                 |
|-----------|----------|--------|---------------------------------------------------------------------------------------|
| `pattern` | yes      | string | The file(s) to validate. The input expects a path to a single file or a glob pattern. |


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


## Contributing

Contributions to this project are welcome. Clone this repository, create a new branch, make your changes, commit them and send in a pull request.

If unsure whether the changes you are proposing would be welcome, open an issue first to discuss your proposal.


## Copyright and License

The phpcsstandards/xmllint-validate GitHub Action is ©copyright PHPCSStandards and contributors and licensed for use under the terms of the MIT License (MIT).
Please see [LICENSE](LICENSE) for more information.
