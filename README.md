## Scenario

There are two Dockefiles in this repo.  One of them (service/Dockerfile) uses
the other (base/Dockerfile) as its base image.

This should be all set up for workspace `AEIB5886C`.

* run `./bump.clj` (executable - requires bb installation) to increment a
  version to increment the version of base/Dockerfile and push
* AWS Code Build is setup to see this push and to build and push two images
  (from base/Dockerfile and service/Dockerfile)
* resulting Image tagged with `latest` and pushed to
  `$AWS_ACCOUNT_ID.dkr.ecr.us-east-1.amazonaws.com`.
* AWS EventBridge is set up to send webhook notifiations back to Atomist
* labels `org.opencontainers.image.revision` and
  `org.opencontainers.image.source` have been added to the builds

Besides pinning and linking, we should also see re-pinning pull requests on the
service Dockerfile each time the base Dockerfile image is pushed.
