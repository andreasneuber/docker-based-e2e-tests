# Docker Based End-to-End Tests

## Idea. What does this do?
We want to run end-to-end tests in a GitLab pipeline using Docker-in-Docker (DinD).
- The "application under test" runs in a Docker container.  
- The tests also run in a separate Docker container and are directed at the 'application under test' container.
- The test report is copied from the test container into the build directory of the GitLab pipeline and saved as an artifact.

## Steps
- Create a docker container with your application under test (see Dockerfile in https://github.com/andreasneuber/automatic-test-sample-site)
- Create a docker container with your tests (see Dockerfile in https://github.com/andreasneuber/playwright-cucumber-js-example)
- Try out if the two containers work well together (see compose.yml in https://github.com/andreasneuber/playwright-cucumber-js-example)

### If so...
- Build and push the two containers into [GitLab container registry](https://docs.gitlab.com/ee/user/packages/container_registry/build_and_push_images.html)
- Create two variables `$TEST_SITE_CONTAINER` and `$TEST` in GitLab settings, values are the containers listed in the [Container Registry](https://gitlab.com/andreasneuber/ruby-cucumber-selenium-framework/container_registry)
- Run a pipeline using `.gitlab-ci.yml`

### Creating/Refreshing Docker image of a GitLab repo via a pipeline
```
image: docker:latest

services:
  - docker:dind

variables:
  DOCKER_DRIVER: overlay2
  DOCKER_TLS_CERTDIR: ""

stages:
  - build

build_image:
  stage: build
  script:
    - docker build -t $CI_REGISTRY_IMAGE:latest .
    - docker login -u $CI_REGISTRY_USER -p $CI_JOB_TOKEN $CI_REGISTRY
    - docker push $CI_REGISTRY_IMAGE:latest

```

## Links
- [Docker Compose - How to execute multiple commands?](https://stackoverflow.com/questions/30063907/docker-compose-how-to-execute-multiple-commands)
- [GitLab artifacts](https://docs.gitlab.com/ee/ci/jobs/job_artifacts.html)
