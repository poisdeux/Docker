# Docker image to build and test Kore

Docker image to build and test [Kore](https://github.com/xbmc/Kore).

## Build

1. Install [Docker](https://www.docker.com/)
2. Get the source from Github
3. Run: `docker build -t kore Docker/Kore`

## Run

To start interactive shell on the Kore docker image run:

```
docker run -it kore /bin/bash
```

## Test

1. Start an interactive shell on the docker image
2. Get latest commits
```git pull```
3. Run local unit/integration tests
```./gradlew testFullDebugUnitTest```
