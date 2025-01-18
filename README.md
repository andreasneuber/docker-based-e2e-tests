# Docker Based UI Tests

## Idea. What does this do?
We want to run UI tests in a Gitlab pipeline using Docker in Docker (DinD).
- The "application under test" runs in a Docker container.  
- The tests itself run also in a Docker container and are directed to the "application under test" container.
- The test report is being copied from the tests container into the build directory of the GitLab pipeline and saved as artifact.

## Steps
- Create a docker container with your application under test (see Dockerfile in https://github.com/andreasneuber/automatic-test-sample-site)
- Create a docker container with your tests (see Dockerfile in https://github.com/andreasneuber/playwright-cucumber-js-example)
- Try out if the two containers work well together (see compose.yml in https://github.com/andreasneuber/playwright-cucumber-js-example)

### If so...
- Build and push the two containers into [GitLab container registry](https://docs.gitlab.com/ee/user/packages/container_registry/build_and_push_images.html)
- Create two variables `$TEST_SITE_CONTAINER` and `$TEST` in GitLab settings, values are the containers listed in the [Container Registry](https://gitlab.com/andreasneuber/ruby-cucumber-selenium-framework/container_registry)
- Run a pipeline using `.gitlab-ci.yml`

## Links
- [Docker Compose - How to execute multiple commands?](https://stackoverflow.com/questions/30063907/docker-compose-how-to-execute-multiple-commands)
- [GitLab artifacts](https://docs.gitlab.com/ee/ci/jobs/job_artifacts.html)
