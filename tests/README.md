# Test Documentation

The tests for this action runner consist of three parts:
1. The `.github/workflows/test.yml` workflow.
2. "Local" test fixtures in the `tests/fixtures` directory.
3. "Remote" tests fixtures in the `docs/tests/` directory.

The `docs` directory is set up to be deployed to a GH Pages website on https://.... to ensure there are downloadable files for use in the tests.
