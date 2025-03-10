<!---
NOTE: AUTO-GENERATED FILE
to edit this file, instead edit its template at: ./github/scripts/templates/README.md.j2
-->
<div align="center">


## Containers

_A heavily opinionated collection of container images_

</div>

<div align="center">

![GitHub Repo stars](https://img.shields.io/github/stars/mrkhachaturov/containers?style=for-the-badge)
![GitHub forks](https://img.shields.io/github/forks/mrkhachaturov/containers?style=for-the-badge)
![GitHub Workflow Status (with event)](https://img.shields.io/github/actions/workflow/status/mrkhachaturov/containers/release-scheduled.yaml?style=for-the-badge&label=Scheduled%20Release)

</div>

<div align="center">

[![OpenSSF Scorecard](https://api.securityscorecards.dev/projects/github.com/mrkhachaturov/containers/badge)](https://securityscorecards.dev/viewer/?uri=github.com/mrkhachaturov/containers)

</div>

Welcome to @mrkhachaturov' container images, if looking for a container start by [browsing the Packages tab in GitHub for this repo](https://github.com/mrkhachaturov?tab=packages&repo_name=containers).

## Mission statement

The containers found in this repo have similar baseline goals to the ones found in [onedr0p's containers repo](https://github.com/onedr0p/containers).

However, the containers found in this repo are more opinionated for my (@mrkhachaturov) use.

For example, using distroless base images, or adding on packages/plugins that fit my use case (e.g. Caddy plugins, installing smbclient packages on NextCloud, changing out the web servers on frontend containers from Nginx to Caddy), etc.

I (@mrkhachaturov) make no guarantees that the containers found here will work for everyone else, **as long as it works for me and fulfils my uses**, I consider it "stable and tested". If you understand that, feel free to use them too!

## Tag immutability

The containers built here do not use immutable tags, as least not in the more common way you have seen from [linuxserver.io](https://fleet.linuxserver.io/) or [Bitnami](https://bitnami.com/stacks/containers).

We do take a similar approach but instead of appending a `-ls69` or `-r420` prefix to the tag we instead insist on pinning to the sha256 digest of the image, while this is not as pretty it is just as functional in making the images immutable.

| Container                                                                 | Immutable  |
|---------------------------------------------------------------------------|------------|
| `registry.mrkhachaturov.tech/mrkhachaturov/gotosocial:rolling`                    | ❌         |
| `registry.mrkhachaturov.tech/mrkhachaturov/gotosocial:0.12.2.1507`                | ❌         |
| `registry.mrkhachaturov.tech/mrkhachaturov/gotosocial:rolling@sha256:8053...`     | ✅         |
| `registry.mrkhachaturov.tech/mrkhachaturov/gotosocial:0.12.2.1507@sha256:8053...` | ✅         |

_If pinning an image to the sha256 digest, tools like [Renovate](https://github.com/renovatebot/renovate) support updating the container on a digest or application version change._

## Passing arguments to a application

Some applications do not support defining configuration via environment variables and instead only allow certain config to be set in the command line arguments for the app. To circumvent this, for applications that have an `entrypoint.sh` read below.

1. First read the Kubernetes docs on [defining command and arguments for a Container](https://kubernetes.io/docs/tasks/inject-data-application/define-command-argument-container/).
2. Look up the documentation for the application and find a argument you would like to set.
3. Set the argument in the `args` section, be sure to include `entrypoint.sh` as the first arg and any application specific arguments thereafter.

    ```yaml
    args:
      - /entrypoint.sh
      - --port
      - "8080"
    ```

## Configuration volume

For applications that need to have persistent configuration data the config volume is hardcoded to `/config` inside the container. This is not able to be changed in most cases.

## Available Images

Each Image will be built with a `rolling` tag, along with tags specific to it's version. Available Images Below

Container | Channel | Image | Latest Tags
--- | --- | --- | ---
[k8s-crd-extractor]() | stable | registry.mrkhachaturov.tech/mrkhachaturov/k8s-crd-extractor |


### Automated tags

Here's an example of how tags are created in the GitHub workflows, be careful with `metadata.json` as it does affect the outcome of how the tags will be created when the application is built.

| Application     | Channel   | Stable  | Base    | Generated Tag                    |
|-----------------|-----------|---------|---------|----------------------------------|
| `ubuntu`        | `focal`   | `true`  | `true`  | `ubuntu:focal-rolling`           |
| `ubuntu`        | `focal`   | `true`  | `true`  | `ubuntu:focal-19880312`          |
| `alpine`        | `3.16`    | `true`  | `true`  | `alpine:rolling`                 |
| `alpine`        | `3.16`    | `true`  | `true`  | `alpine:3.16.0`                  |
| `gotosocial`    | `develop` | `false` | `false` | `gotosocial-develop:0.12.2.1538` |
| `gotosocial`    | `develop` | `false` | `false` | `gotosocial-develop:rolling`     |
| `gotosocial`    | `main`    | `true`  | `false` | `gotosocial:0.12.2.1507`         |
| `gotosocial`    | `main`    | `true`  | `false` | `gotosocial:rolling`             |

## Deprecations

Containers here can be **deprecated** at any point, this could be for any reason described below.

1. The upstream application is **no longer actively developed**
2. The upstream application has an **official upstream container** that follows closely to the mission statement described here
3. The upstream application has been **replaced with a better alternative**
4. The **maintenance burden** of keeping the container here **is too bothersome**

**Note**: Deprecated containers in this repo may be removed at any time. Hopefully procrastination will keep the deprecated containers long enough.

## Credits

This repo's main pipeline code (found in `.github`) was taken from [onedr0p's containers repo](https://github.com/onedr0p/containers). Full attributions can be found in the `.github/CREDITS.md`.