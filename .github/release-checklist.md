# Release checklist

## Before Release

- [ ] Verify the documentation in the README is up to date.
- [ ] Prepare a human readable changelog for the release based on the tickets in the milestone.

## Release

- [ ] Fast-forward the `v#` branch for the current major to the latest commit on the `develop` branch (or merge `develop` into `v#`).
- [ ] Make sure all CI builds are green.
- [ ] Tag and create a release (careful, GH defaults to `develop`!) & add the changelog to it.
    Tags should use the `v` prefix!
- [ ] Close the milestone.
- [ ] Open a new milestone for the next release.
- [ ] If any open PRs/issues which were milestoned for this release did not make it into the release, update their milestone.
- [ ] Fast-forward `develop` to be equal to `v#`.

## Publicize

- [ ] Post on Mastodon about the release.
- [ ] Post on X about the release.
- [ ] Post on LinkedIn.
