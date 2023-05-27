# Harness CD Setup and Usage guideline

[Harness](https://www.harness.io/) is the industry’s first Software Delivery Platform to use AI to simplify your DevOps processes - CI, CD & GitOps, Feature Flags, Cloud Costs, and much more.

Follow below steps to install, configure and use Harness on Mac M2

## Prerequisite

On M2 Chip, we need to install Rosetta which enables a Mac with Apple silicon to use apps built for a Mac with an Intel processor.

```
$ /usr/sbin/softwareupdate --install-rosetta --agree-to-license
```

## Installation and Configuration

Clone harness repo and provision all necessary services using docker-compose

```
$ git clone https://github.com/harness/harness-cd-community.git

$ cd harness-cd-community/docker-compose/harness

$ docker-compose up -d
```

Running `docker-compose ps` should show the below services provisioned.

![image](https://github.com/narramadan/gotchas/assets/3821456/bfb1a2d9-584a-479f-881e-1c665a5f18ff)



## Cleanup

Run below command to stop and remove containers ans networks

```
$ docker-compose down
```

Delete unused images

```
$ docker image prune -a
```
