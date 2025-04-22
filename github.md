# Developing Pressio Repositories

This guide is tailored to the three core Pressio libraries,
namely [pressio-rom](https://github.com/Pressio/pressio-rom),
[pressio-ops](https://github.com/Pressio/pressio-ops), and
[pressio-log](https://github.com/Pressio/pressio-log),
although the general principles hold for all Pressio
repositories.

Jump to:

- [SSH and GPG Verification](#ssh-and-gpg-verification)
- [Cloning the Repositories](#cloning-the-repositories)
- [Header-Only Development](#header-only-development)
- [Testing](#testing)
- [Macros and Preprocessing Directives](#macros-and-preprocessing-directives)
    - [Caveat for Testing](#caveat-for-testing)

---

### SSH and GPG Verification

All Pressio developers should set up
[SSH and GPG keys](https://github.com/settings/keys) for
their GitHub account.

All commits should be signed:

```
git config --global commit.gpgsign true
```

### Cloning the Repositories

Always clone Pressio repositories with SSH. For example:

```
git clone git@github.com:Pressio/pressio-rom.git
```

### Header-Only Development

The three core Pressio libraries are all header-only,
meaning that there is no need to build or install the
source code.

Therefore, the top-level `CMakeLists.txt` files for each
repository are sparse and only exist to optionally enable
the tests (which will be discussed subsequently).
As a rule of thumb, nothing else should be added to the
top-level `CMakeLists.txt`.

### Testing

Unlike the source code, the tests need
to be built. They are essentially standalone apps
that must include the header files from the Pressio library.
To build the tests, configure the library to enable testing.
The CMake variable is different for each library, but will
be something like:

```sh
cd /path/to/build
cmake -D PRESSIO_ENABLE_TESTING=ON /path/to/source
```

> [!NOTE]
> The tests for `pressio-rom` depend on `pressio-ops`.
> When building the tests, `pressio-ops` will be cloned
> automatically. If you'd like to use your local
> `pressio-ops`, just set the `-D PRESSIO_OPS_INCLUDE_DIR`
> CMake variable.

### Macros and Preprocessing Directives

Because Pressio is designed with various third-party
libraries in mind (e.g. Trilinos, Eigen, and Kokkos),
we use macros to enable or disable code specific to
certain libraries.

For example, an application that uses Kokkos datatypes with
Pressio would define, before including any Pressio headers,
the following macro:

```cpp
#define PRESSIO_ENABLE_TPL_KOKKOS
```

Throughout the Pressio source code, Kokkos-specific code is
guarded by

```cpp
#ifdef PRESSIO_ENABLE_TPL_KOKKOS
// Kokkos-specific code here
#endif
```

#### Caveat for testing

When building the tests, these TPL macros can be passed
as CMake variables to enable or disable tests for each
TPL. For example, to build the Kokkos tests, configure
the tests with:

```sh
cd /path/to/build
cmake \
    -D PRESSIO_ENABLE_TESTS=ON \
    -D PRESSIO_ENABLE_TPL_KOKKOS=ON \
    /path/to/source
```

### Issues and Pull Requests

Generally, development should target a specific issue.
Before beginning work on a new feature in a repository,
open an issue and create a branch for it.

> [!NOTE]
> All branches should originate from `develop`.

Pull requests may be opened at any point in the development
process to get feedback from other developers; if your code
is not yet ready for reviews, just be sure to mark it as
`Draft` in GitHub.

> [!TIP]
> If the repository does not support Draft Pull Requests,
> simply put `DRAFT` in the PR title to make it clear that
> it is a work in progress.

In the PR description, reference the number of the issue
resolved by the PR:

```
Fixes #<issue-number>
```

This will ensure that the issue is automatically closed
when the PR is merged.

Make sure that your pull request targets the `develop`
branch (if it exists). Pushes to `main` are generally
reserved for releases.

After a pull request is merged, the corresponding issue
should be closed and the feature branch should be deleted.
These should happen automatically, as long as the PR
description properly references the issue number.
