---
title: deck file add-plugins
source_url: https://github.com/Kong/deck/tree/main/cmd
content_type: reference
---

Add plugins to objects in a decK file.

The plugins are added to all objects that match the selector expressions. If no
selectors are given, the plugins are added to the top-level `plugins` array.

The plugin files have the following format (JSON or YAML) and are applied in the
order they are given:

    { "_format_version": "1.0",
      "add-plugins": [
        { "selectors": [
            "$..services[*]"
          ],
          "overwrite": false,
          "plugins": [
            { "name": "my-plugin",
              "config": {
                "my-property": "value"
              }
            }
           ],
        }
      ]
    }

## Syntax

```
deck file add-plugins [command-specific flags] [global flags] [...plugin-files]
```

## Flags

`--config`
:  JSON snippet containing the plugin configuration to add. Repeat to add
multiple plugins.

`--format`
:  Output format: JSON or YAML. (Default: `"YAML"`)

`-h`, `--help`
:  Help for add-plugins.

`-o`, `--output-file`
:  Output file to write. Use `-` to write to stdout. (Default: `"-"`)

`--overwrite`
:  Specify this flag to overwrite plugins by the same name if they already
exist in an array. The default behavior is to skip existing plugins. (Default: `false`)

`--selector`
:  JSON path expression to select plugin-owning objects to add plugins to.
Defaults to the top level (selector `$`). Repeat for multiple selectors.

{:.important}
> **Warning**: The JSONPath implementation has a known issue related to 
recursive descent with expressions. Expressions following a recursive
descent do not work as expected, however, a workaround is available by preceding the
expression with a wildcard selection. For example, `$..plugins[?(@.regex_priority>100)]` must
be expressed as `$..plugins[*][?(@.regex_priority>100)]`. See the 
[go-apiops library documentation](https://github.com/Kong/go-apiops/blob/main/docs/README.md#notes) 
for details on this issue.

`-s`, `--state`
:  decK file to process. Use `-` to read from stdin. (Default: `"-"`)


## Global flags

`--analytics`
:  Share anonymized data to help improve decK.
Use `--analytics=false` to disable this. (Default: `true`)

`--ca-cert`
:  Custom CA certificate (raw contents) to use to verify Kong's Admin TLS certificate.
This value can also be set using DECK_CA_CERT environment variable.
This takes precedence over `--ca-cert-file` flag.

`--ca-cert-file`
:  Path to a custom CA certificate to use to verify Kong's Admin TLS certificate.
This value can also be set using DECK_CA_CERT_FILE environment variable.

`--headers`
:  HTTP headers (key:value) to inject in all requests to Kong's Admin API.
This flag can be specified multiple times to inject multiple headers.

`--kong-addr`
:  HTTP address of Kong's Admin API.
This value can also be set using the environment variable DECK_KONG_ADDR
 environment variable. (Default: `"http://localhost:8001"`)

`--kong-cookie-jar-path`
:  Absolute path to a cookie-jar file in the Netscape cookie format for auth with Admin Server.
You may also need to pass in as header the User-Agent that was used to create the cookie-jar.

`--konnect-addr`
:  Address of the Konnect endpoint. (Default: `"https://us.api.konghq.com"`)

`--konnect-email`
:  Email address associated with your Konnect account.

`--konnect-password`
:  Password associated with your Konnect account, this takes precedence over `--konnect-password-file` flag.

`--konnect-password-file`
:  File containing the password to your Konnect account.

`--konnect-runtime-group-name`
:  Konnect Runtime group name.

`--konnect-token`
:  Personal Access Token associated with your Konnect account, this takes precedence over `--konnect-token-file` flag.

`--konnect-token-file`
:  File containing the Personal Access Token to your Konnect account.

`--no-color`
:  Disable colorized output (Default: `false`)

`--skip-workspace-crud`
:  Skip API calls related to Workspaces (Kong Enterprise only). (Default: `false`)

`--timeout`
:  Set a request timeout for the client to connect with Kong (in seconds). (Default: `10`)

`--tls-client-cert`
:  PEM-encoded TLS client certificate to use for authentication with Kong's Admin API.
This value can also be set using DECK_TLS_CLIENT_CERT environment variable. Must be used in conjunction with tls-client-key

`--tls-client-cert-file`
:  Path to the file containing TLS client certificate to use for authentication with Kong's Admin API.
This value can also be set using DECK_TLS_CLIENT_CERT_FILE environment variable. Must be used in conjunction with tls-client-key-file

`--tls-client-key`
:  PEM-encoded private key for the corresponding client certificate .
This value can also be set using DECK_TLS_CLIENT_KEY environment variable. Must be used in conjunction with tls-client-cert

`--tls-client-key-file`
:  Path to file containing the private key for the corresponding client certificate.
This value can also be set using DECK_TLS_CLIENT_KEY_FILE environment variable. Must be used in conjunction with tls-client-cert-file

`--tls-server-name`
:  Name to use to verify the hostname in Kong's Admin TLS certificate.
This value can also be set using DECK_TLS_SERVER_NAME environment variable.

`--tls-skip-verify`
:  Disable verification of Kong's Admin TLS certificate.
This value can also be set using DECK_TLS_SKIP_VERIFY environment variable. (Default: `false`)

`--verbose`
:  Enable verbose logging levels
Sets the verbosity level of log output (higher is more verbose). (Default: `0`)

## See also

* [deck file](/deck/{{page.kong_version}}/reference/deck_file)   - Sub-command to host the decK file manipulation operations

