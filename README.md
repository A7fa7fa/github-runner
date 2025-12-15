# github-runner

adapted from [https://testdriven.io/blog/github-actions-docker/](https://testdriven.io/blog/github-actions-docker/)

start.sh is set as entrypoint and registers and authorizes with github

## start up

Get your version and checksum from https://github.com/actions/runner/releases. 

Populate env file and build image.

```bash
export RUNNER_VERSION=2.316.1
export VALIDATION_HASH=0dbc9bf5a58620fc52cb6cc0448abcca964a8d74b5f39773b7afcad9ab691e19
docker build -t github-runner:latest --build-arg RUNNER_VERSION=$RUNNER_VERSION --build-arg VALIDATION_HASH=$VALIDATION_HASH .

```
Start the build image
```bash
docker run --name github-runner --env-file ./.env -d github-runner:latest

```

or let compose handle everything
```bash
docker-compose up --build
```

ensure the runner has correct permission to docker host machine
```bash
sudo usermod -aG docker $(whoami)
optional
chmod 666 /var/run/docker.sock
```
