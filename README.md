# Pl000139PlanningAndAdviceServices

This project was generated using [Nx](https://nx.dev).

<p align="center"><img src="https://raw.githubusercontent.com/nrwl/nx/master/nx-logo.png" width="450"></p>

**Nx is a set of Extensible Dev Tools for Monorepos.**

## Repository Setup

##### Dependencies

1. Node 14
2. Set your script shell to bash  
   `npm config set script-shell "C:\\Program Files\\Git\\bin\\bash.exe"`
   * Windows users may install https://www.cygwin.com/ for GNU and Open Source tools which provide functionality similar to a Linux distribution on Windows.
   * Note: Using bash shell will avoid false negative warnings thrown by @fmr-pr103625/fmr-apmtracer postinstall script. Maintainers of the library have been notified. If you don't use bash and you see a message regarding its postinstall.js, you can safely proceed.
3. Install Nrwl command line interface  
   `npm i -g @nrwl/cli`

##### Steps

1. Create a personal access token in Stash:  
   https://confluence.atlassian.com/bitbucketserver/personal-access-tokens-939515499.html
   (Set "Write" permission at minimum for personal access token to be able to create PR)
2. Set the token in your global git config  
   `git config --global stash.token <token>`
3. Install node modules  
   `npm ci`
4. Review the code review documentation below before starting any development

## Code review process

Code reviews are an important part of our development process, read more below:

* Review the monorepo [code review process](docs/code_review_process.md)
* Review the process for [creating a pull request](docs/pull_request_guidelines.md)
* Reference the [code review guidelines and checklist for reviewers](docs/code_review_guidelines.md)
* Watch the [discussion about code review process](http://fidvid.fmr.com/watch?id=esc_program%3A379041)

## Important Links
* [Confluence](https://confluence.fmr.com/pages/viewpage.action?pageId=454071357)
* [Jenkins CI](https://itec-jenkins.fmr.com/cm304/job/PI/job/PL000139/job/PR109650/job/AwsCloud-uDeploy-Pipelines/job/PNA-MONOREPO-ECS/job/pna-monorepo-ci/)
* [Jenkins CD](https://itec-jenkins.fmr.com/cm304/job/PI/job/PL000139/job/PR109650/job/AwsCloud-uDeploy-Pipelines/job/PNA-MONOREPO-ECS/job/pna-monorepo-cd/)

## Generators

### Workspace

Run the following generators using the following command in terminal:

`nx workspace-generator <name>`

| name      | description                                                                      |
| --------- | -------------------------------------------------------------------------------- |
| create-pr | Opens a pull request from the currently checked out branch into an origin branch |
| create-client-app | Generates an Angular application, a domain, and a feature |
| create-api-app | Generates a Nest application under a domain with optional GraphQL integration |
| create-api-e2e | Generates cypress e2e for api-app |
| create-types | Generates typescript files from GraphQl definition files |
| create-domain | Generates DDD domain library |
| create-feature | Generates DDD feature library |

### Nx Plugins

Run the following generators using the following command in terminal:

`nx g <name>`

| name      | description                                                             | documentation |
| --------- | ----------------------------------------------------------------------- | ------------- |
| @nrwl/angular:storybook-configuration | Add storybook configuration to a ui library | https://nx.dev/latest/angular/plugins/storybook/schematics/configuration |
| @nrwl/angular:stories | Create stories/specs for all components declared in a library | https://nx.dev/latest/node/plugins/angular/schematics/stories |

## Local environment variables

### Node apps
To setup local node environment variables add a .env file to your applications root directory formatted like below. 

Think of this .env file as your Smaas configuration. Environment (PROD, XQ1, QA1 ect) specific variables should NEVER be defaulted in your source code ( eg tokenSeceret = process.env.TOKEN || 'Token') regardless of sensitivity. Doing this can mask issues in lower environments that don't popup until moving to PROD.

```
// sample .env

ENVIRONMENT=QA1
APP_ID=AP135579
APP_NAME=AP135727-COST-ESTIMATOR-API
OAUTH_CLIENT_ID=myClientId
OAUTH_CLIENT_SECRET=myClientSecret
```

Loading these variables is built into Nx and more detail on how these are loaded can be found [here](https://nx.dev/angular/cli/overview#loading-environment-variables)

### Angular apps
This setup is for local development only and is used to add FEBSEC headers to outgoing requests from your angular app.

**Configuration setup is documented [here](./tools/local/febsec-proxy/readme.md)**

## Npm Install vs Npm CI
* Use npm install if you have updated or added a new dependency. **This commit should include package-lock.json**
* When you run npm install double check that the package-lock.json package references are pointing to artifactory and not npmjs registry
* Use npm ci if you just cloning or reinstalling modules or for use in the CI pipelines

## How to migrate Nx workspace versions

[Nx release notes](https://github.com/nrwl/nx/releases)

1. Discuss updating Nx versions in weekly monorepo meeting and agree upon the version
2. Ensure all the @nrwl packages in package.json DO NOT have ranged versions (~ or ^)
3. Follow this [guide](https://nx.dev/latest/angular/core-concepts/updating-nx#how-to-migrate) to migrate.
4. Commit migration changes
5. Ensure build, lint, and test targets are passing for all apps/libs
6. Ensure storybook is working properly (nx storybook shared-storybook)

## Quick Start & Documentation

[Nx Documentation](https://nx.dev/angular)

[10-minute video showing all Nx features](https://nx.dev/angular/getting-started/what-is-nx)

[Interactive Tutorial](https://nx.dev/angular/tutorial/01-create-application)

## Development server

Run `ng serve my-app` for a dev server. Navigate to http://localhost:4200/. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng g component my-component --project=my-app` to generate a new component.

## Build

Run `ng build my-app` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test my-app` to execute the unit tests via [Jest](https://jestjs.io).

Run `nx affected:test` to execute the unit tests affected by a change.

## Running end-to-end tests

Run `ng e2e my-app --type=(open|run) --config=(local|dit|qa1|xq1) --tags=(@Smoke|@Regression)` to execute the end-to-end tests via [Cypress](https://www.cypress.io).

Run `nx affected:e2e --type=(open|run) --config=(local|dit|qa1|xq1) --tags=(@Smoke|@Regression)` to execute the end-to-end tests affected by a change.

## Understand your workspace

Run `nx dep-graph` to see a diagram of the dependencies of your projects.

## Further help

Visit the [Nx Documentation](https://nx.dev/angular) to learn more.

## Style Guide

### Angular
1. [Routing](docs/angular/routing.md)
2. [Templates](docs/angular/templates.md)
3. [Components](docs/angular/components.md)
