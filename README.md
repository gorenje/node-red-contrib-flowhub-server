## FlowHub Local Server

**Local Git storage for Node-RED flows**

This package defines the flows that are required to install and run a local Git store for the usage with the FlowHub.org [node package](https://flows.nodered.org/node/@gregoriusrippenstein/node-red-contrib-flowhub).

The aim is to enable local git usage for maintaining visual flow code using a visual version control approach based on Git.

This work was inspired by the [Local First Conf](https://www.localfirstconf.com/).

This installs **no** nodes nor plugins, the package only provides example flows that, when installed, provide the backend for the FlowHub.org nodes. This package is slightly larger (ca. 20MB) but that's because it contains third-party JS code for the Webiliser frontend.

That allows this to be executed completely offline, including the Webiliser frontend.

## Installation

Using the Flow Importer interface inside of Node-RED to install these flows via the examples list of flows.

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

## Using SSL Certificates

There is a [post](https://discourse.nodered.org/t/setup-of-https-ssl-local-webxr-quest-development/96224) describing how to do that for Node-RED.



