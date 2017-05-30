# Docker Buildkite Plugin ![Build status](https://badge.buildkite.com/3a4b0903b26c979f265c049c932fb4ff3c055af7a199a17216.svg)

A [Buildkite](https://buildkite.com/) plugin for running pipeline steps in [Docker](https://www.docker.com/) containers

If you need more control, please see the [docker-compose Buildkite Plugin](https://github.com/buildkite-plugins/docker-compose-buildkite-plugin).

The docker container has the host buildkite-agent binary mounted in to `/usr/bin/buildkite-agent` and the required environment variables set. 

## Example

The following pipeline will run `yarn install` and `yarn run test` inside a Docker container using the [node:7 Docker image](https://hub.docker.com/_/node/):

```yml
steps:
  - command: yarn install && yarn run test
    plugins:
      docker#v1.0.0:
        image: "node:7"
        workdir: /app
```

## Configuration

### `image` (required)

The name of the Docker image to use.

Example: `node:7`

### `workdir` (required)

The working directory where the pipeline’s code will be mounted to, and run from, inside the container.

Example: `/app`

### `buildkite-agent-bin` (optional)

The path on the host for `buildkite-agent`. If not set, defaults to to `buildkite-agent` from the `$PATH`. 

If set to `false` then no agent binary will be mounted and no env will be passed to the container. Make sure to pass this as a string, otherwise YAML will interpret it incorrectly.

## License

MIT (see [LICENSE](LICENSE))