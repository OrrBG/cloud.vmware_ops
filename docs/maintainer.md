# Docs For Maintainers

This describes the actions required for maintainers of the repo, as well as any other things that might be useful to know.

## Releases

Release versions follow the semver versioning pattern. To create a new release:

1. Install `antsibull-docs` via pip
2. Create a new branch on your fork, usually called `release/<new version>`
3. Increment the collection version in the `galaxy.yml`
4. Run `antsibull-changelog release`. This will delete the changelog fragments and write the new changelog to `CHANGELOG.rst`.
5. Commit the changes with the commit message `release <new version>`
6. Open a PR to merge the release branch into main.

Once the PR has been merged:

7. Use the Github UI to create a new release. You must tag main with the new version number. The tag is just the version number, not `v0.0.0`
8. Pull the new version of main. You can do a `git reset --hard HEAD` and `git clean -dfx` if you have any extra files present. You do not want any extra files present.
9. Build the collection, `ansible-galaxy collection build .`. This will create a tar file.
10. Optionally, inspect the tar file to make sure no extra files were included: `tar -tf <tar file name>`
11. Upload the new tar file to Automation Hub only. Do not upload to Galaxy.

### Supporting Ansible Core Versions

When a version of Ansible core is no longer supported by the repo, you need to update the documentation (`README.md`), remove the version from the execution environment `execution-environment/execution-environment.yml`, and update the minimum version in `meta/runtime.yml`. Deprecating a version is a major version change.

## Testing

Testing is done as a part of the pull request workflow. There are a few key tests:
- unit tests
- integration tests, run against a simulated vCenter (container) and an actual vCenter (Eco-vCenter)
- sanity tests (includes a variety of linters)

### Pre-Commit

Pre-commit hooks are available using the `pre_commit` python package. Hooks must be enabled by the developer using `pre-commit install` or disabled using `pre-commit uninstall`. Hooks are optional.

## Tools

`prepare_symlinks.yml` - this is used by the integration tests
