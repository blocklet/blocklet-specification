# Blocklet Meta Specification

This document describes how to define a blocklet that can be find/installed/managed by **ABT Node**.

## Basic Requirements

- A blocklet meta file is noted as `blocklet.yml` within the root directory of the published blocklet tarball.
- A blocklet can only be published and consumed in a blocklet bundle format, ABT Node does not helps on blocklet bundling
- A blocklet registry can aggregate meta information of many blocklets to make it easier to find/publish blocklets

## Blocklet Definition

| Field                          | Type     | Required? | Description                                               | Memo                                                                                               | Status |
| ------------------------------ | -------- | --------- | --------------------------------------------------------- | -------------------------------------------------------------------------------------------------- | ------ |
| did                            | String   | Yes       | The DID of the blocklet                                   | Derived from blocklet name                                                                         |        |
| name                           | String   | Yes       | The name of the blocklet                                  | Usually in snake case                                                                              |        |
| title                          | String   | No        | The human readable name of the blocklet                   | Defaults to title if not specified                                                                 |        |
| description                    | String   | Yes       | The description of the blocklet                           | Displayed in marketplace                                                                           |        |
| version                        | String   | Yes       | The version of the blocklet                               | Should be versioned according to [semver](https://semver.org/)                                     |        |
| group                          | Enum     | Yes       | The type of the blocklet, can be `dapp/static`            | Critical for ABT Node to decide how to mange the blocklet                                          |        |
| provider                       | Enum     | Yes       | The provider of the blocklet, can be `arcblock/community` | Just for display purpose                                                                           |        |
| main                           | String   | Yes       | The entry point of the blocklet                           | Should point to the static folder for static blocklets, and the executable file for dapp blocklets |        |
| public_url                     | String   | No        | The public interface of the blocklet                      | Should point to an accessible URL when the blocklet is running                                     |        |
| admin_url                      | String   | No        | The admin interface of the blocklet                       | Should point to an accessible URL when the blocklet is running                                     |        |
| config_url                     | String   | No        | The configuration interface of the blocklet               | Should point to an accessible URL when the blocklet is running                                     |        |
| doc_url                        | String   | No        | The documentation interface of the blocklet               | Should point to an accessible URL when the blocklet is running                                     |        |
| logo                           | String   | No        | The logo of the blocklet                                  | Should point to a file in blocklet package                                                         |        |
| keywords                       | [String] | No        | The keywords of the blocklet                              | Parsed from `package.json`                                                                         |        |
| author                         | String   | No        | The author info of the blocklet, name, email, etc         | Parsed from `package.json`                                                                         |        |
| support                        | String   | No        | How to get support with the blocklet                      | Parsed from `package.json`                                                                         |        |
| homepage                       | String   | No        | Home page of the blocklet                                 | Parsed from `package.json`                                                                         |        |
| community                      | String   | No        | URL of the blocklet community                             | Such as https://community.arcblockio.cn                                                            |        |
|                                |          |           |                                                           |                                                                                                    |        |
| hooks                          | Object   | No        | Defines blocklet lifecycle scripts                        |                                                                                                    |        |
| hooks.pre_install              | String   | No        | Script to run before install the blocklet                 | Can use this to check environment requirements                                                     |        |
| hooks.pre_deploy               | String   | No        | Script to run before deploy the blocklet                  | Can use this to build blocklets                                                                    |        |
| hooks.pre_start                | String   | No        | Script to run before start the blocklet                   | Can use this to prepare some data for the blocklet                                                 |        |
| hooks.pre_stop                 | String   | No        | Script to run before stop the blocklet                    | Can use this to do some cleanup for the blocklet                                                   |        |
| hooks.pre_uninstall            | String   | No        | Script to run before uninstall the blocklet               | Can use this to do some cleanup for the blocklet                                                   |        |
|                                |          |           |                                                           |                                                                                                    |        |
| repository                     | Object   | No        | Defines blocklet source location                          |                                                                                                    |        |
| repository.type                | String   | No        | Repository type, can be `git`                             |                                                                                                    |        |
| repository.url                 | String   | No        | Repository URL                                            |                                                                                                    |        |
|                                |          |           |                                                           |                                                                                                    |        |
| charging                       | Object   | No        | A place holder for charging related                       |                                                                                                    |        |
| charging.price                 | Number   | No        | The price of the blocklet, default to 0                   |                                                                                                    |        |
|                                |          |           |                                                           |                                                                                                    |        |
| stats                          | Object   | No        | A place holder for statistics related                     |                                                                                                    |        |
| stats.downloads                | Number   | No        | The download count                                        | Parsed from npm registry                                                                           |        |
| stats.updated_at               | Date     | No        | Last update time                                          | Parsed from npm registry                                                                           |        |
|                                |          |           |                                                           |                                                                                                    |        |
| capabilities                   | Object   | No        | Blocklet capabilities                                     |                                                                                                    |        |  |  |
| capabilities.dynamicPathPrefix | Boolean  | No        | Can the blocklet be served from any dynamic path prefix   | Default true                                                                                       |        |
|                                |          |           |                                                           |                                                                                                    |        |
| requiredEnvironments           | [Object] | No        | Runtime configuration that can be customized for blocklet |                                                                                                    |        |  |  |
| environment.name               | String   | Yes       | The configuration name                                    |                                                                                                    |        |
| environment.description        | String   | Yes       | The configuration description                             |                                                                                                    |        |
| environment.required           | String   | No        | Is the config required                                    |                                                                                                    |        |
| environment.default            | String   | No        | The default value of the config                           |                                                                                                    |        |
|                                |          |           |                                                           |                                                                                                    |        |
| scripts                        | Object   | No        | For `abtnode dev`                                         |                                                                                                    |        |  |  |
| scripts.dev                    | String   | Yes       | Command to start the blocklet in dev mode                 |                                                                                                    |        |
|                                |          |           |                                                           |                                                                                                    |        |
| engine                         | [Object] | No        | For none-node.js blocklets                                |                                                                                                    |        |  |  |
| engine.interpretor             | String   | Yes       | Command to start the blocklet in production mode          | Support interpretors are whitelisted in ABT Node                                                   |        |
| engine.script                  | String   | Yes       | Script to start the blocklet in production mode           | Should point to a file in blocklet bundle                                                          |        |
| engine.args                    | String   | Yes       | Arguments to start the blocklet script                    |                                                                                                    |        |
| engine.platform                | String   | No        | Which platform can use this script                        |                                                                                                    |        |

## Blocklet DID Generation

> TODO

## Blocklet Bundle Process

> TODO

| Metadata |                  |
| -------- | ---------------: |
| Version  |            0.0.1 |
| Status   | Work in progress |
| Created  |       2020-11-03 |
