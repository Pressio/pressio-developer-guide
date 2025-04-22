# Pressio Containers

All Pressio repositories use the same [Docker
containers](https://www.docker.com/resources/what-container/)
in their testing pipelines.

This way, we can ensure compatibility among all of the
various libraries in the Pressio ecosystem and reduce
time maintaining separate containers for each repository.

The containers are stored in the [GitHub Container
Registry](https://github.com/orgs/Pressio/packages)
of the Pressio organization.

The Dockerfiles that generate these containers are kept
in the [pressio-containers](https://github.com/Pressio/pressio-containers)
repository. Any change to a container must be made
to the corresponding Dockerfile as a PR in this repo.

> [!NOTE]
> The names of the containers are purposely general.
> To see the dependencies and versions used in each
> container, examine the corresponding Dockerfile
> in the [containers](https://github.com/Pressio/pressio-containers/tree/main/docker_scripts)
> repository.

The [README](https://github.com/Pressio/pressio-containers/blob/main/README.md) of the containers repository includes
instructions for updating existing containers and adding
new ones.
