# Pressio Developer Guide

The Pressio ecosystem comprises multiple libraries
designed to facilitate the implementation of reduced-order models
(ROMs) in large-scale applications.

This guide provides information on how to develop Pressio. Because
the ecosystem is modular, we will start by providing an overview
of the key repositories in the Pressio organization.

## Core Pressio Repositories

There are three primary libraries that make up Pressio:

- [pressio-rom](https://github.com/Pressio/pressio-rom): Implementation of the core ROM functionality
- [pressio-ops](https://github.com/Pressio/pressio-ops): Generic operations for common linear algebra software libraries
- [pressio-log](https://github.com/Pressio/pressio-log): Lightweight logging functionality for Pressio repositories

All of these libraries are **header-only**. Further, the version numbers of these repositories
are synced, such that any given version of `pressio-rom` is guaranteed to be compatible
with the same version of both `pressio-ops` and `pressio-log`.

## Additional Repositories

Other repositories in the Pressio ecosystem include:

- [pressio-containers](https://github.com/Pressio/pressio-containers): All Docker containers used in CI testing
- [pressio-demoapps](https://github.com/Pressio/pressio-demoapps): Suite of sample problems
- [pressio-tutorials](https://github.com/Pressio/pressio-tutorials): Demonstrations of integrating Pressio with the sample problems from `pressio-demoapps`
- [Pressio.github.io](https://github.com/Pressio/Pressio.github.io): Content for the top-level [Pressio website](https://pressio.github.io/).

## Guides

Development of the three [core Pressio repositories](#core-pressio-repositories) is closely connected.
The first three guides explain how developers of those libraries can push code, publish releases,
and update the Spack packages.

### [1. GitHub Workflow](https://github.com/Pressio/pressio-developer-guide/blob/main/github.md)

The `GitHub Workflow` guide explains how to clone any of the core Pressio repositories, how they are
designed, and how to open pull requests to implement changes.

### [2. Releases](https://github.com/Pressio/pressio-developer-guide/blob/main/releases.md)

The `Releases` guide enumerates the steps to prepare and publish a new release of any of the core
Pressio repositories.

### [3. Spack](https://github.com/Pressio/pressio-developer-guide/blob/main/spack.md)

The `Spack` guide shows how to update the existing `spack` packages from each core Pressio repository.
This should be done after every new release.

---

### [4. Containers](https://github.com/Pressio/pressio-developer-guide/blob/main/containers.md)

All of the Docker containers used in CI throughout the Pressio ecosystem are defined in the
[pressio-containers](https://github.com/Pressio/pressio-containers) repository. This guide
explains how to update these containers and add new ones.
