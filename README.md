# Two Docker Containers in Gitlab Pipeline

## Steps
- Create a docker container for your application under test (see Dockerfile here https://github.com/andreasneuber/automatic-test-sample-site)
- Create a docker container with your tests (see Dockerfile here https://github.com/andreasneuber/playwright-cucumber-js-example)
- Try out if the two containers work well together (see compose.yml here https://github.com/andreasneuber/playwright-cucumber-js-example)

If so...
- Build and push the two containers into [Gitlab container registry](https://docs.gitlab.com/ee/user/packages/container_registry/build_and_push_images.html)
- Create two variables `$TEST_SITE_CONTAINER` and `$TEST` in Gitlab settings, values are the containers listed in the Container [Registry](https://gitlab.com/andreasneuber/ruby-cucumber-selenium-framework/container_registry)
- Run a pipeline

## Links
- [Docker Compose - How to execute multiple commands?](https://stackoverflow.com/questions/30063907/docker-compose-how-to-execute-multiple-commands)
- [Gitlab artifacts](https://docs.gitlab.com/ee/ci/jobs/job_artifacts.html)
