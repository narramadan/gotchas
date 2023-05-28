# Harness CI/CD Setup, Configuration and Usage guideline on Mac M2

[Harness](https://www.harness.io/) is the industry’s first Software Delivery Platform to use AI to simplify your DevOps processes - CI, CD & GitOps, Feature Flags, Cloud Costs, and much more.

Follow below steps to install, configure and use Harness on Mac M2

## Prerequisite

On M2 Chip, we need to install Rosetta which enables a Mac with Apple silicon to use apps built for a Mac with an Intel processor.

```
$ /usr/sbin/softwareupdate --install-rosetta --agree-to-license
```
Enable the below configurations in Docker Desktop, which will enable using Rosetta on M2.

![image](https://github.com/narramadan/gotchas/assets/3821456/cc0078a2-7e96-4d3e-827e-805aa09062ae)

![image](https://github.com/narramadan/gotchas/assets/3821456/63e49ae1-fa99-492f-8283-e8f0b4cf41ee)

## Installation and Configuration

### Harness CI

Harness CI Community Edition (aka [Drone](https://www.drone.io/)) is a modern Continuous Integration platform to automate their build, test and release workflows using a powerful, cloud native pipeline engine.

TODO

### Harness CD

Clone harness repo and provision all necessary services using docker-compose

```
$ git clone https://github.com/harness/harness-cd-community.git

$ cd harness-cd-community/docker-compose/harness

$ docker-compose up -d
```

Running `docker-compose ps` should show the below services provisioned.

![image](https://github.com/narramadan/gotchas/assets/3821456/bfb1a2d9-584a-479f-881e-1c665a5f18ff)

## Usage

Open http://localhost/#/signup and complete the registration form to start using Harness CD. Signed up user will be created as admin user.

We should be able to access the webpage post signup

![image](https://github.com/narramadan/gotchas/assets/3821456/8e907265-900a-4636-99cc-3a8c4f84cfcf)


## Cleanup

Run below command to stop and remove containers ans networks

```
$ docker-compose down
```

Delete unused images

```
$ docker image prune -a
```

## Troubleshooting

### 502 Bad Gateway Error

if Harness signup page is failing with `502 Bad Gateway`, then follow [instructions](https://github.com/harness/harness-cd-community/issues/79) to comment out `mongo` configuration in `docker-compose.yml` file.

## Resources

* https://medium.com/@jccguimaraes/run-a-drone-ci-pipeline-locally-f4bfb4741c53
* https://medium.com/globant/introduction-to-drone-io-ci-cd-platform-1d43f8bc1728
