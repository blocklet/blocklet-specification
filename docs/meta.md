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

| Field                     | Type          | Required? | Description                                                       | Memo                                                                                                   | Status |
| ------------------------- | ------------- | --------- | ----------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------ | ------ |
| `did`                     | String        | Yes       | The DID of the blocklet                                           | Derived from blocklet name and represents the immutable decentralized identity address of the Blocklet | Draft  |
| `name`                    | String        | Yes       | The name of the blocklet                                          | Usually in snake_case                                                                                  | Final  |
| `title`                   | String        | No        | The human readable name of the blocklet                           | Defaults to title if not specified                                                                     | Final  |
| `description`             | String        | Yes       | The description of the blocklet                                   | Displayed in marketplace                                                                               | Final  |
| `version`                 | String        | Yes       | The version of the blocklet                                       | Should be versioned according to [semver](https://semver.org/)                                         | Final  |
| `group`                   | Enum          | Yes       | The type of the blocklet, can be `dapp/static`                    | Critical for ABT Node to decide how to mange the blocklet                                              | Draft  |
| `category`                | Enum          | Yes       | The category of the blocklet                                      | Not implemented yet                                                                                    | TODO   |
| `main`                    | String        | Yes       | The entry point of the blocklet                                   | Should point to the static folder for static blocklets, and the executable file for dapp blocklets     | TODO   |
| `logo`                    | String        | No        | The logo of the blocklet                                          | Should point to a file in blocklet package                                                             | Final  |
| `keywords`                | [String]      | No        | The keywords of the blocklet                                      | Parsed from `package.json`                                                                             | Final  |
| `author`                  | String        | Yes       | The author info of the blocklet, ex. name, email, etc             | Parsed from `package.json`                                                                             | Final  |
| `support`                 | String        | No        | How to get support with the blocklet                              | Parsed from `package.json`                                                                             | Final  |
| `homepage`                | String        | No        | Home page of the blocklet                                         | Parsed from `package.json`                                                                             | Final  |
| `community`               | String        | No        | URL of the blocklet community                                     | Such as https://community.arcblockio.cn                                                                | Final  |
| `gitHash`                 | String        | No        | Git commit hash of current blocklet release                       | Should be set by bundle tools                                                                          | Final  |
|                           |               |           |                                                                   |                                                                                                        |        |
| `files`                   | [String]      | No        | Files to be included in the blocklet bundle                       | Default blocklet related files are included automatically, such as `blocklet.js/zip/md`                | Final  |
|                           |               |           |                                                                   |                                                                                                        |        |
| `interfaces`              | [Object]      | Yes       |                                                                   |                                                                                                        | Final  |
| `interface.type`          | Enum          | Yes       | The type of the interface                                         | Can be `web` or `service`                                                                              | Final  |
| `interface.name`          | String        | Yes       | The name of the interface                                         | Must be unique within the blocklet                                                                     | Final  |
| `interface.path`          | String        | Yes       | The pathname of the interface                                     | Default to `/`                                                                                         | Final  |
| `interface.prefix`        | String        | No        | Does the interface support dynamic path prefix                    | Can be `*` or any valid path name, `*` means dynamic path prefix is supported                          | Final  |
| `interface.port`          | String/Object | No        | Which port the interface is served from the blocklet              | If the port is specified with a string, it's the port name, default to `BLOCKLET_PORT`                 | Final  |
| `interface.port.internal` | Number        | No        | Which port the interface is served from the blocklet              | If the port is specified with a string, it's the port name                                             | Final  |
| `interface.port.external` | Number        | No        | Which port the service should be exposed on                       | If the port is specified with a object, it is required                                                 | Final  |
| `scripts`                 | Object        | No        | Defines blocklet lifecycle scripts                                |                                                                                                        | Final  |
| `scripts.dev`             | String        | No        | Script to run the blocklet in dev mode                            | Must be set if you want users to run `abtnode dev` with your blocklet                                  | Final  |
| `scripts.preInstall`      | String        | No        | Script to run before install the blocklet                         | Can use this to check environment requirements                                                         | Final  |
| `scripts.preDeploy`       | String        | No        | Script to run before deploy the blocklet                          | Can use this to build blocklets                                                                        | Final  |
| `scripts.preStart`        | String        | No        | Script to run before start the blocklet                           | Can use this to prepare some data for the blocklet                                                     | Final  |
| `scripts.preStop`         | String        | No        | Script to run before stop the blocklet                            | Can use this to do some cleanup for the blocklet                                                       | Final  |
| `scripts.preUninstall`    | String        | No        | Script to run before uninstall the blocklet                       | Can use this to do some cleanup for the blocklet                                                       | Final  |
| `signatures`              | [Object]      | Yes       | List of signatures containing developers, Blocklet registry, etc. | The first signature is at the end of the array                                                         | Draft  |
| `signatures.type`         | String        | Yes       | Signature Algorithm                                               |                                                                                                        | Draft  |
| `signatures.name`         | String        | Yes       | Name of the signer                                                |                                                                                                        | Draft  |
| `signatures.signer`       | String        | Yes       | DID address of the signer                                         | The format is Base58                                                                                   | Draft  |
| `signatures.pk`           | String        | Yes       | Public key of the signer                                          | The format is base58                                                                                   | Draft  |
| `signatures.excludes`     | [String]      | No        | Fields that are not involved in the current signature             | If there are fields not involved in the current signature, the `excludes` field is required            | Draft  |
| `signatures.appended`     | [String]      | No        | Fields added by the current signer                                | If there are fields are added by the current signer, the `appended` field is required                  | Draft  |
| `signatures.created`      | String        | Yes       | Time of signature                                                 | The format is `ISO 8601`                                                                               | Draft  |
| `signatures.sig`          | String        | Yes       | Signature signed by current signer                                | The format is `Base58`                                                                                 | Draft  |
| `repository`              | Object        | No        | Defines blocklet source location                                  |                                                                                                        | Final  |
| `repository.type`         | String        | No        | Repository type, can be `git`                                     |                                                                                                        | Final  |
| `repository.url`          | String        | No        | Repository URL                                                    |                                                                                                        | Final  |
| `environments`            | [Object]      | No        | Runtime configuration that can be customized for blocklet         |                                                                                                        | Final  |
| `environment.name`        | String        | Yes       | The configuration name                                            |                                                                                                        | Final  |
| `environment.description` | String        | Yes       | The configuration description                                     |                                                                                                        | Final  |
| `environment.required`    | String        | No        | Is the config required                                            |                                                                                                        | Final  |
| `environment.default`     | String        | No        | The default value of the config                                   |                                                                                                        | Final  |
| `environment.secure`      | Boolean       | No        | Whether the config is secure                                      |                                                                                                        | Final  |
| `environment.validation`  | String        | No        | How to validate the env                                           |                                                                                                        | TODO   |
| `timeout`                 | Object        | No        | Timeout configuration for blocklet                                |                                                                                                        | Final  |
| `timeout.start`           | Number        | No        | Blocklet start timeout in seconds                                 | Default to 10 seconds, max allowed is 600 seconds                                                      | Final  |
| `requirements`            | [Object]      | No        | Runtime configuration that can be customized for blocklet         |                                                                                                        | Final  |
| `requirements.abtnode`    | String        | No        | Required abtnode version to run on                                | Default to ">=v1.1.0"                                                                                  | Final  |
| `requirements.os`         | String        | No        | Required os to run on                                             | Default to "\*", can be list of value from `process.platform`                                          | Final  |
| `requirements.cpu`        | String        | No        | Required cpu architecture to run on                               | Default to "\*", can be list of value from `process.arch`                                              | Final  |
| `scripts`                 | [Object]      | No        | For none-node.js blocklets                                        |                                                                                                        | Draft  |
| `script.name`             | Enum          | Yes       | `dev/start/build`                                                 | Should point to a file in blocklet bundle                                                              | Draft  |
| `script.command`          | String        | Yes       | Script to start the blocklet in production mode                   | Should point to a file in blocklet bundle                                                              | Draft  |
| `script.platform`         | String        | No        | `mac/linux`                                                       |                                                                                                        | Draft  |

> For integrity generating and verifying, we can leverage the [ssri](https://www.npmjs.com/package/ssri) package.

## Blocklet Registry Extras

Following fields are appended to the blocklet meta after blocklet published to registry.

| Field                | Type   | Required? | Description                                      | Memo                                                                                        | Status |
| -------------------- | ------ | --------- | ------------------------------------------------ | ------------------------------------------------------------------------------------------- | ------ |
| `dist`               | Object | No        | Blocklet distribution info                       |                                                                                             | Final  |
| `dist.tarball`       | String | Yes       | URL to download the blocklet tarball             | Can use underlying npm registry, but can support any valid url                              | Final  |
| `dist.integrity`     | String | Yes       | Used to verify the download                      | Refer to [SRI](https://developer.mozilla.org/en-US/docs/Web/Security/Subresource_Integrity) | Final  |
| `dist.file_count`    | Number | Yes       | Files included in the bundle                     |                                                                                             | Draft  |
| `dist.unpacked_size` | Number | Yes       | Size on disk of the package when unpacked.       |                                                                                             | Draft  |
| `charging`           | Object | No        | A place holder for charging related requirements |                                                                                             | Draft  |
| `charging.price`     | Number | No        | The price of the blocklet, default is 0          |                                                                                             | Draft  |
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
| Version  |            0.0.2 |
| Status   | Work in progress |
| Created  |       2020-11-03 |
| Updated  |       2020-11-24 |
