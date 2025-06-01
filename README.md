# pytest_exmon

## Release Process

### Release Draft

- When a branch is merged into the main branch the `release-drafter` github action workflow will be started.
- This workflow will record the merged branches that have not been captured by a previous release, into a new draft release version.
- The draft release content should be reviewed to ensure all changes are required into the release.
- Sections and the merged PR's under them are controlled by git labels.

### Release

1. Be on a branch.

    If a single branch is to be published as a release then be on that branch else create a new branch. E.g.

    ```shell
    git switch -c release_v1.0.0
    ```

2. Run tbump.

    Use the following command to bump the versions but not apply the git tag.

    ```shell
    # poetry run tbump <REQUIRED_VERSION> --only-patch
    poetry run tbump 1.0.0 --only-patch
    ```

3. Commit changes.

    Review, add the changed files, commit and push.

    ```shell
    git status
    git add pyproject.toml
    git add qa_pytest_framework/__init__.py
    git add tbump.toml
    git commit -m "release v1.0.0"
    git push origin <branch-name>
    ```

4. Create the PR and seek approval.

    In github, create a PR for the branch you just pushed and get it reviewed and approved. Once approved, merge it in.

5. Apply git tag.

    Switch to main branch, get latest and apply git tag.

    ```shell
    git switch main
    git pull origin main
    git tag --annotate v1.0.0 --message "Release v1.0.0"
    git push --tag
    ```

6. Review release.

    In github, the Actions can be monitoring to ensure they succeeded.
