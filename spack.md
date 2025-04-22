# Updating the Pressio Spack Packages

After new releases of the Pressio libraries, the corresponding Spack packages must be updated.

Jump to:
- [Clone the Pressio/spack repository](#1-clone-the-pressiospack-repository)
- [Update the `package.py` files](#2-update-the-packagepy-files)
- [Test the packages locally](#3-test-the-packages-locally)
- [Open a pull request](#4-open-a-pull-request)

---

### 1. Clone the Pressio/spack repository

Begin by cloning the Pressio fork of the Spack repository:

```sh
git clone git@github.com:Pressio/spack.git
```

Create a new branch off of `develop` with the new version.
For example, for version 0.16.0:

```
git checkout -b add-pressio-version-0.16.0 develop
```

### 2. Update the `package.py` files

All Spack packages are defined in `spack/var/spack/repos/builtin/packages`.

From this directory, there are folders for `pressio-rom`,
`pressio-ops`, and `pressio-log`, all containing their own
`package.py` file that defines the Spack package.

In all three `package.py` files, add the new version:

```python
    version("main", branch="main")
    version("0.15.0", branch="0.15.0")
    # Add new versions here
```

As more versions are added, it may be useful to switch
to using a `for` loop:

```python
    supported_versions = ["main", "0.15.0", ...]
    for v in supported_versions:
        version(v, branch=v)
```

> [!NOTE]
> The `pressio-rom` package uses this loop syntax instead
> of directly defining every version.

The existing logic in the `pressio-rom` package ensures
that any given version of `pressio-rom` is only compatible
with the exact same version of `pressio-ops`
and `pressio-log`.

For example, `pressio-rom@0.15.0` will only use
`pressio-ops@0.15.0` and `pressio-log@0.15.0`.

### 3. Test the packages locally

To make sure everything works correctly, it is best to test
the updated packages before pushing to the Spack repository.

Start by sourcing the forked Spack's setup script:

```
source <path-to-pressio-spack>/share/spack/setup-env.sh
```

Then you can check the info of the Spack packages to see
the new version. For example:

```
spack info pressio-rom
```

Installing `pressio-rom@<new-version>` should also install
the new versions of `pressio-ops` and `pressio-log`.

For example, to test version 0.16.0:

```
spack install pressio-rom@0.16.0
```

If you make any changes to the `package.py` files, refresh
the Spack package index with:

```
spack reindex
```

Then uninstall any previously installed packages with

```
spack uninstall --all
```

### 4. Open a pull request

Once everything works locally, commit your changes with a
descriptive commit name prefaced with `pressio: ...`.
For example, `pressio: add version 0.16.0`.

Then push your local branch to the Pressio fork of Spack:

```
git push --set-upstream origin <branch-name>
```

Then, from GitHub, go to the Pressio/spack repository and
open a new pull request. Be sure it is targeting the
`develop` branch of the **original** Spack repository.

```
spack:develop  <-- Pressio:<branch-name>
```

The title of the pull request should be **"Pressio: add version X.X.X"** (with the correct version
number).

### 5. Wait for reviews/merge

The package maintainers will automatically be requested for
reviews, and a Spack developer will also review and merge
once it is ready.
