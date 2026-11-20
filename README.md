<!-- markdownlint-disable MD041 -->
<!-- markdownlint-disable MD033 -->
<!-- markdownlint-disable MD028 -->

<!-- PROJECT SHIELDS -->
<!--
*** I'm using markdown "reference style" links for readability.
*** Reference links are enclosed in brackets [ ] instead of parentheses ( ).
*** See the bottom of this document for the declaration of the reference variables
*** for contributors-url, forks-url, etc. This is an optional, concise syntax you may use.
*** https://www.markdownguide.org/basic-syntax/#reference-style-links
-->

[![pre-commit][pre-commit-shield]][pre-commit-url]
[![taskfile][taskfile-shield]][taskfile-url]

# composer.strg.at

Private static composer registry powered by [composer/satis][satis-url].

<details>
  <summary style="font-size:1.2em;">Table of Contents</summary>

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [Automation](#automation)
  - [build and deploy](#build-and-deploy)
- [Structure](#structure)
- [Requirements](#requirements)
- [Development](#development)
  - [Configuration](#configuration)
  - [Getting Started](#getting-started)
  - [Pre-commit](#pre-commit)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->
</details>

## Automation

### build and deploy

[![build-deploy][build-deploy-badge]][build-deploy-url]

- The workflow can be triggered manually (click the badge for more).
- The workflow runs on Monday morning and on each push to `main` that changes `satis.json`.
- The `strg-satis` GitHub App token reads the private repositories.
- The `strg-public-bot` GitHub App token commits the build output to `main`.

## Structure

```console
└── satis.json                              # satis configuration
```

## Requirements

- [docker][docker-url] (development)
- [python3][python-url] (development)
- [task][taskfile-url] (development)

## Development

### Configuration

You will need a [GITHUB_TOKEN][gh-pat-url].

You can either input the token interactive when running `task satis:build` or create a file in `.composer/auth.json`.

```json
{
  "github-oauth": {
    "github.com": "$GITHUB_TOKENs" // add your token here
  }
}
```

### Getting Started

To build the static assets run:

```console
task satis:build
```

To start a local server run:

```console
task satis:serve
```

### Pre-commit

To enable pre-commit you can run:

```console
task pre-commit:init
```

To lint/check all files with pre-commit:

```console
task pre-commit:run
```

<!-- MARKDOWN LINKS & IMAGES -->
<!-- https://www.markdownguide.org/basic-syntax/#reference-style-links -->

<!-- Links -->

[satis-url]: https://github.com/composer/satis
[docker-url]: https://www.docker.com/
[python-url]: https://www.python.org/
[gh-pat-url]: https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token
[build-deploy-url]: https://github.com/strg-at/satis-registry/actions/workflows/build-deploy.yaml

<!-- Badges -->

[pre-commit-shield]: https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit
[pre-commit-url]: https://github.com/pre-commit/pre-commit
[taskfile-url]: https://taskfile.dev/
[taskfile-shield]: https://img.shields.io/badge/Taskfile-Enabled-brightgreen?logo=task
[build-deploy-badge]: https://github.com/strg-at/satis-registry/actions/workflows/build-deploy.yaml/badge.svg?branch=main
