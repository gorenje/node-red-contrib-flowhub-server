## Local Git Store for Node-RED

**Local Git storage for Node-RED flows**

This package defines the flows that are required to install and run a local Git store for the usage with the FlowHub.org [node package](https://flows.nodered.org/node/@gregoriusrippenstein/node-red-contrib-flowhub).

The aim is to enable local git usage for maintaining visual flow code using a visual version control approach based on Git.

This installs **no** nodes nor plugins, the package only provides example flows that, when installed, provide the backend for the FlowHub.org nodes. This package is slightly larger (ca. 20MB) but that's because it contains third-party JS code for the Webiliser frontend.

That allows this to be executed completely offline, including the Webiliser frontend.

## Introduction

FlowHub.org provides *visual* change management (aka version control) on top of GitHub. FlowHub Local (aka FlowHubⓁ) is a local-first server for the FlowHub.org nodes, replacing the GitHub requirement.

FlowHubⓁ provides a local gitstore for managing change made to flows, locally, no internet connection is required. FlowHubⓁ is used in conjunction with the FlowHub.org nodes but provides a local gitstore, replacing GitHub.

FlowHubⓁ has a client-server architecture with both client and server being installed in Node-RED instances. The [client](https://flows.nodered.org/node/@gregoriusrippenstein/node-red-contrib-flowhub) and [server](https://flows.nodered.org/node/@gregoriusrippenstein/node-red-contrib-flowhub-server) are both Node-RED node packages that can be installed into any Node-RED instance.

FlowHubⓁ is designed to be installed on a central instance of Node-RED and multiple clients connect and communicate with that installation of FlowHubⓁ.

This solution was inspired by the [Local First Conf](https://www.localfirstconf.com/) initiative.

## Installation

Installation is described in the [installation guide](https://cdn.openmindmap.org/content/FlowHub-local-installation-guide.pdf).

## FlowHub.org Token definition

To use this backend server, the [FlowHub.org nodes](https://flows.nodered.org/node/@gregoriusrippenstein/node-red-contrib-flowhub) need a token that points to this server. This requires that the hostname of the server needs to be added to the token.

Tokens for local servers always begin with `local://` followed by the hostname of Node-RED hosting the backend `examples/flowhub-local-server.json` flow.

For example, a valid local token would be:

```
local://https://gitstore:1880/store/gerrit/screencast1/main
```

Explanation:

- `local://` is the token prefix for a local token, c.f., a FlowHub.org remote token is prefixed with `fhb_`.
- the Node-RED host is reached via `https://gitstore:1880`. HTTPS isn't required but is recommended.
- `/store/` is the path specified needs to be included
- `gerrit/screencast1/main` is the username to commit changes with, screencast1 is the repository name which corresponds to the directory name in the repos directory. `main` is the branch and should be used by default.

## Changes to settings.js

Some changes need to be made to the `settings.js` file to support the larger flow size.


```
    /** The maximum size of HTTP request that will be accepted by the runtime api.
     * Default: 5mb
     */
    //apiMaxLength: '5mb',
```

because of the size of the CDN flow, this needs to be changed to at least 25mb 

```
    /** The maximum size of HTTP request that will be accepted by the runtime api.
     * Default: 5mb
     */
    apiMaxLength: '25mb',
```

## Using SSL Certificates

There is a [post](https://discourse.nodered.org/t/setup-of-https-ssl-local-webxr-quest-development/96224) describing how to do that for Node-RED.

