# Contributing

## How to contribute

* File issues.
* Edit/write documentation.
* Submit pull requests.
* Test in different environments.
* Raise awareness.

## Summary of tools

Following tools are getting used:

* `Angular` as primary target framework http://angular.io/
* `TypeScript` as primary language - https://www.typescriptlang.org/
* `ng-packagr` to generate Angular specific package format - https://github.com/dherges/ng-packagr
* `compodoc` for API documentation - https://compodoc.app/
* `Jasmine` for test cases - https://jasmine.github.io/
* `Karma` for running test cases in browsers - http://karma-runner.github.io/
* `nodejs` during development - https://nodejs.org/
* `npm` for dependency management, packaging and distribution - https://www.npmjs.com/
* `git` for version control - https://git-scm.com/

## Initial setup

Instructions on setting up development environment:

* Install `node` and `npm` - https://nodejs.org/
* Checkout code from GitHub - you may fork the code first into your GitHub account.
* Use `npm i` to install dependencies:
    ```bash
    $ npm i
    ```

## Project structure

The project was originally generated by angular-cli (at Angular 2).
In those days there was no clear guideline on how to create and organize an
Angular library.
Later it switched to `ng-packagr` which brought quite a lot of sanity.
The source code is in `src` folder.
All the test case files are within `specs` which is not what typically Angular
projects do.

Because of compatibility reasons paths of specific files have been kept same.
While doing v8 - when v6 compatibility would be dropped, the source code is
likely to be rearranged.

## Setup a Stomp broker

* A Stomp broker is used for running the tests. I have been using RabbitMQ.
* Edit `spec/config/browser-config.js` and `spec/config/node-config.js` as per
  your setup. Defaults should work for as RabbitMQ default setup on localhost.
* Please note that in RabbitMQ you will need to enable Stomp and WebStomp plugins.
* By default RabbitMQ WebStomp will treat messages a text, you will need to tell
  it is use binary frames:
    ```bash
    $ echo 'web_stomp.ws_frame = binary' >> /etc/rabbitmq/rabbitmq.conf
    ```
* A RabbitMQ Dockerfile is provided with necessary plugins and configuration. To use it, run:
    ```bash
    $ docker build -t myrabbitmq rabbitmq/ # Needed only once
    $ docker run -d -p 15674:15674 myrabbitmq # to start the broker
    ```

## Building and testing

Key npm tasks:

```text
cleanup - Remove generated built artifacts
doc - Generate docs
doc-serve - Generate docs and watch for changes
test - Run tests
lint - run lint on soucres
```

### Basic development workflow

1. Checkout a new branch.
1. Make code changes (src/specs)
1. Run tests:
    ```bash
    $ npm run test
    ```
1. Lint:
    ```bash
    $ npm run lint
    ```
1. Update documentation - do update the docs-src/Changelog.md
1. Regenerate documentation:
    ```bash
    $ npm run doc
    ```
1. Please follow GitHub guidelines. Raise an issue if you are unclear.