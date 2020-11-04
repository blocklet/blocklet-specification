---
TOCTitle: Blocklet Meta Specification
PageTitle: blocklet.yml reference
MetaDescription: Blocklet Meta Specification and blocklet.yml reference
DateApproved:
---

# Blocklet Meta Specification

This document describes how to define a blocklet that can be find/installed/managed by **ABT Node**.

## Basic Requirements

- A blocklet meta file is noted as `blocklet.yml` within the root directory of the published blocklet tarball.
- A blocklet can only be published and consumed in a blocklet bundle format, ABT Node does not help with blocklet bundling.
- A blocklet registry can aggregate meta information of many blocklets to make it easier to find/publish blocklets.

## Blocklet Definition

| Field                            | Type     | Required? | Description                                               | Memo                                                                                                   | Status |
| -------------------------------- | -------- | --------- | --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ------ |
| `did`                            | String   | Yes       | The DID of the blocklet                                   | Derived from blocklet name and represents the immutable decentralized identity address of the Blocklet | TODO   |
| `name`                           | String   | Yes       | The name of the blocklet                                  | Usually in snake_case                                                                                  | Final  |
| `title`                          | String   | No        | The human readable name of the blocklet                   | Defaults to title if not specified                                                                     | Final  |
| `description`                    | String   | Yes       | The description of the blocklet                           | Displayed in marketplace                                                                               | Final  |
| `version`                        | String   | Yes       | The version of the blocklet                               | Should be versioned according to [semver](https://semver.org/)                                         | Final  |
| `group`                          | Enum     | Yes       | The type of the blocklet, can be `dapp/static`            | Critical for ABT Node to decide how to mange the blocklet                                              | Remove |
| `provider`                       | Enum     | Yes       | The provider of the blocklet, can be `arcblock/community` | Just for display purposes                                                                              | Remove |
| `main`                           | String   | Yes       | The entry point of the blocklet                           | Should point to the static folder for static blocklets, and the executable file for dapp blocklets     | TODO   |
| `logo`                           | String   | No        | The logo of the blocklet                                  | Should point to a file in blocklet package                                                             | Final  |
| `keywords`                       | [String] | No        | The keywords of the blocklet                              | Parsed from `package.json`                                                                             | Final  |
| `author`                         | String   | No        | The author info of the blocklet, ex. name, email, etc     | Parsed from `package.json`                                                                             | Final  |
| `support`                        | String   | No        | How to get support with the blocklet                      | Parsed from `package.json`                                                                             | Final  |
| `homepage`                       | String   | No        | Home page of the blocklet                                 | Parsed from `package.json`                                                                             | Final  |
| `community`                      | String   | No        | URL of the blocklet community                             | Such as https://community.arcblockio.cn                                                                | Final  |
|                                  |          |           |                                                           |                                                                                                        |        |
| `interfaces`                     |          |           |                                                           |                                                                                                        | Draft  |
| `interfaces.public`              | String   | No        | The public interface of the blocklet                      | Should point to an accessible URL when the blocklet is running                                         | Draft  |
| `interfaces.admin`               | String   | No        | The admin interface of the blocklet                       | Should point to an accessible URL when the blocklet is running                                         | Draft  |
| `interfaces.config`              | String   | No        | The configuration interface of the blocklet               | Should point to an accessible URL when the blocklet is running                                         | Draft  |
| `interfaces.doc`                 | String   | No        | The documentation interface of the blocklet               | Should point to an accessible URL when the blocklet is running                                         | Draft  |
|                                  |          |           |                                                           |                                                                                                        |        |
| `exposedService`                 |          |           |                                                           |                                                                                                        | Draft  |
| `service.protocol`               | Enum     | No        | The public interface of the blocklet                      | Should point to an accessible URL when the blocklet is running                                         | Draft  |
| `service.port`                   | Number   | No        | The admin interface of the blocklet                       | Should point to an accessible URL when the blocklet is running                                         | Draft  |
| `service.upstreamPort`           | Number   | No        | The configuration interface of the blocklet               | Should point to an accessible URL when the blocklet is running                                         | Draft  |
|                                  |          |           |                                                           |                                                                                                        |        |
| `hooks`                          | Object   | No        | Defines blocklet lifecycle scripts                        |                                                                                                        | Final  |
| `hooks.pre_install`              | String   | No        | Script to run before install the blocklet                 | Can use this to check environment requirements                                                         | Final  |
| `hooks.pre_deploy`               | String   | No        | Script to run before deploy the blocklet                  | Can use this to build blocklets                                                                        | Final  |
| `hooks.pre_start`                | String   | No        | Script to run before start the blocklet                   | Can use this to prepare some data for the blocklet                                                     | Final  |
| `hooks.pre_stop`                 | String   | No        | Script to run before stop the blocklet                    | Can use this to do some cleanup for the blocklet                                                       | Final  |
| `hooks.pre_uninstall`            | String   | No        | Script to run before uninstall the blocklet               | Can use this to do some cleanup for the blocklet                                                       | Final  |
| `hookFiles` --> `files`          | [String] | No        | List of hook files to be bundled                          | Should not be empty if hooks is not empty                                                              | Final  |
|                                  |          |           |                                                           |                                                                                                        |        |
| `repository`                     | Object   | No        | Defines blocklet source location                          |                                                                                                        | Final  |
| `repository.type`                | String   | No        | Repository type, can be `git`                             |                                                                                                        | Final  |
| `repository.url`                 | String   | No        | Repository URL                                            |                                                                                                        | Final  |
|                                  |          |           |                                                           |                                                                                                        |        |
| `capabilities` --> interfaces    | Object   | No        | Blocklet capabilities                                     |                                                                                                        | TODO   |
| `capabilities.dynamicPathPrefix` | Boolean  | No        | Can the blocklet be served from any dynamic path prefix   | Default true                                                                                           | TODO   |
|                                  |          |           |                                                           |                                                                                                        |        |
| `environments`                   | [Object] | No        | Runtime configuration that can be customized for blocklet |                                                                                                        | Final  |
| `environment.name`               | String   | Yes       | The configuration name                                    |                                                                                                        | Final  |
| `environment.description`        | String   | Yes       | The configuration description                             |                                                                                                        | Final  |
| `environment.required`           | String   | No        | Is the config required                                    |                                                                                                        | Final  |
| `environment.default`            | String   | No        | The default value of the config                           |                                                                                                        | Final  |
| `environment.validation`         | String   | No        | How to validate the env                                   |                                                                                                        | TODO   |
|                                  |          |           |                                                           |                                                                                                        |        |
| `requirements`                   | [Object] | No        | Runtime configuration that can be customized for blocklet |                                                                                                        | TODO   |
| `requirement.type`               | Enum     | No        | `runtime/platform`                                        |                                                                                                        | TODO   |
|                                  |          |           |                                                           |                                                                                                        |        |
| `scripts`                        | [Object] | No        | For none-node.js blocklets                                |                                                                                                        | Draft  |
| `script.name`                    | Enum     | Yes       | `dev/start/build`                                         | Should point to a file in blocklet bundle                                                              | Draft  |
| `script.command`                 | String   | Yes       | Script to start the blocklet in production mode           | Should point to a file in blocklet bundle                                                              | Draft  |
| `script.platform`                | String   | No        | `mac/linux`                                               |                                                                                                        | Draft  |

> For integrity generating and verifying, we can leverage the [ssri](https://www.npmjs.com/package/ssri) package.

## Blocklet Registry Extras

Following fields are appended to the blocklet meta after blocklet published to registry.

| Field                | Type   | Required? | Description                                      | Memo                                                                                        | Status |
| -------------------- | ------ | --------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------- | ------ |
| `dist`               | Object | No        | Blocklet distribution info                       |                                                                                             | Draft  |
| `dist.tarball`       | String | Yes       | URL to download the blocklet tarball             | Can use underlying npm registry, but can support any valid url                              | Draft  |
| `dist.integrity`     | String | Yes       | Used to verify the download                      | Refer to [SRI](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity) | Draft  |
| `dist.file_count`    | Number | Yes       | Files included in the bundle                     |                                                                                             | Draft  |
| `dist.unpacked_size` | Number | Yes       | Size on disk of the package when unpacked.       |                                                                                             | Draft  |
| `dist.registry_pk`   | String | No        | Public key of the registry                       |                                                                                             | Draft  |
| `dist.registry_did`  | String | No        | DID of the registry                              |                                                                                             | Draft  |
| `dist.registry_sig`  | String | No        | Signature for the blocklet by the registry       |                                                                                             | Draft  |
|                      |        |           |                                                  |                                                                                             |        |
| `charging`           | Object | No        | A place holder for charging related requirements |                                                                                             | Draft  |
| `charging.price`     | Number | No        | The price of the blocklet, default is 0          |                                                                                             | Draft  |
|                      |        |           |                                                  |                                                                                             |        |
| `stats`              | Object | No        | A place holder for statistics related info       |                                                                                             | Draft  |
| `stats.downloads`    | Number | No        | The download count                               | Parsed from npm registry                                                                    | Draft  |
| `stats.updated_at`   | Date   | No        | Last update time                                 | Parsed from npm registry                                                                    | Draft  |

## Blocklet DID Generation

1. Take `name` field from blocklet meta
2. Create buffer from name: `Buffer.from(name, 'utf8')`
3. Use buffer as the public-key to generate the did: `fromPublicKey(buffer, { role: types.RoleType.Any })

## Meta

| Metadata |                  |
| -------- | ---------------: |
| Version  |            0.0.1 |
| Status   | Work in progress |
| Created  |       2020-11-03 |
