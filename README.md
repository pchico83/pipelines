# D-Pipelines

D-Pipeline is a docker image specialized to execute docker CI/CD tasks. Some similar tools are:

- [Habitus](https://github.com/cloud66/habitus)
- [Gitlab Runner](http://docs.gitlab.com/ce/ci/yaml/README.html#gitlab-ci-yml)
- [Bitbucket Pipelines](https://confluence.atlassian.com/bitbucket/configure-bitbucket-pipelines-yml-792298910.html)

The key idea behind __D-Pipeline__ is to be optimzed for docker and for easy of use. The only dependency to execute a d-pipeline is to have docker installed.

Pipelines are configured using a __docker-pipeline.yml__ file, whose format is:

```
Pipeline: 
  - stage1
  - ...
  - stageN

Job1:
    Stage: stage1 
    Source: master
    Command: run busybox (only docker commands)
    Condition: always | on_failure | on_success
Job2:
...
JobN
```

- Pipeline: is a list of stages, each stage has a set of jobs executed in parallel and stages are executed in sequence.
- Stage: the stage that the job belongs to. If not provided, the name of the job is the name of the stage.
- Source: for which tag or branches this stage is executed.
- Command: a docker command to be executed.
- Condition: execute the job always, only when the previous stage fails or only when the previous stage succeeds (default: `on_success`).
