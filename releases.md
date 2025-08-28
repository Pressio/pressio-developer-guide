# Creating a New GitHub Release

This section explains how to release a new version of Pressio on GitHub.

Releases of the three core libraries should always be synced, so that, e.g.,
a new release of `pressio-rom` also coincides with the **same version**
release for both `pressio-ops` and `pressio-log`.

### 1. Update version number

The versions of the core Pressio libraries are defined as macros in the following
files:

| Library     | File                 |
| :---------- | :------------------- |
| pressio-rom | `pressio_macros.hpp` |
| pressio-ops | `ops_macros.hpp`     |
| pressio-log | `version.hpp`        |

When updating the version number, be sure to:

1. Bump the version number to the next release or release candidate.
2. Ensure that the lines in the top-level `version.txt` file are accurate.
3. Update the version number of each repository in [Pressio.github.io](https://github.com/Pressio/Pressio.github.io/blob/main/docs/source/index.rst).

### 2. Update main branch

As explained in the [GitHub Workflow](https://github.com/Pressio/pressio-developer-guide/blob/main/github.md)
guide, all three repositories are organized so that the `develop` branch holds all new changes, and `main` is only
updated before a release.

To update the `main` branch with changes, follow these steps:

1. In each repository, create a new **release candidate branch** off of develop (i.e. `pressio-0.15.0-release-candidate`).
2. Verify that all release candidate branches (for all three repositories) are compatible with any external apps that depend on Pressio.
3. Open a pull request to merge the release candidate branch into `main`.
4. Confirm that all CI pipelines pass.
5. Merge the pull request (the release candidate branch can be deleted).

### 3. Publish new release

A new release is published from the `Releases` page of each repository's GitHub:

- pressio-rom [Releases](https://github.com/Pressio/pressio-rom/releases)
- pressio-ops [Releases](https://github.com/Pressio/pressio-ops/releases)
- pressio-log [Releases](https://github.com/Pressio/pressio-log/releases)

From the release page, follow these steps:

1. Select `Draft a New Release`
2. Select `Choose a Tag` and type in the new release number.

> [!NOTE]
> The release tag should only be a number--i.e. `0.15.0` and not `v0.15.0`

3. Set the `Target` branch to `main` (not `develop`).
4. Set the `Release title` to the release number (same as the release tag).
4. Add any release notes.

For all of these steps, view previous releases to see what we've done in the past.

### 4. Update the Spack packages

Once the GitHub releases are done, the Spack packages must be updated to the latest versions.
Instructions for this are included in the [Spack](https://github.com/Pressio/pressio-developer-guide/blob/main/spack.md) guide.
