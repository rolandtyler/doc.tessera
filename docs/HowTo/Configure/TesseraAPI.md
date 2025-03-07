---
description: Configure servers for Tessera API
---

# Configure servers for Tessera API

Configure the [servers for the Tessera API](../../Concepts/TesseraAPI.md) in the
[Tessera configuration file](Tessera.md).

Specify the servers to be started as a list in `serverConfigs`.

```json
"serverConfigs": [
   <server settings>
]
```

## Server Addresses

The server configuration has two address entries:

- `serverAddress` - Address of the server.
  This can be specified as an IP address or a DNS name.
- `bindingAddress` - (optional) Endpoint to use for the binding.
  Specify to bind to an internal IP while advertising an external IP using `serverAddress`.

Each server is individually configured and can advertise over HTTP, HTTPS, or a Unix Socket.

You can also [configure CORS](#configure-cors) for the `ThirdParty` server type.

### HTTP server configuration

=== "HTTP"

    ```json
    {
        "app": "<app type>",
        "enabled": <boolean>,
        "serverAddress":"http://[host]:[port]/[path]",
        "communicationType" : "REST"
    }
    ```

=== "Third Party Example"

    ```json
    {
       "app": "ThirdParty",
       "enabled": true,
       "serverAddress": "http://localhost:9081",
       "communicationType": "REST"
    }
    ```

### HTTPS server configuration

=== "HTTPS"

    ```json
    {
        "app": "<app type>",
        "enabled": <boolean>,
        "serverAddress":"https://[host]:[port]/[path]",
        "communicationType" : "REST",
        "sslConfig": {
            <SSL settings>
        }
    }
    ```

=== "P2P Example"

    ```json
    {
        "app": "P2P",
          "enabled": true,
          "serverAddress": "http://localhost:9001",
          "sslConfig": {
            "tls": "enum STRICT,OFF",
            "generateKeyStoreIfNotExisted": "boolean",
            "serverKeyStore": "Path",
            "serverTlsKeyPath": "Path",
            "serverTlsCertificatePath": "Path",
            "serverKeyStorePassword": "String",
            "serverTrustStore": "Path",
            "serverTrustCertificates": [
              "Path"
            ],
            "serverTrustStorePassword": "String",
            "serverTrustMode": "TOFU",
            "clientKeyStore": "Path",
            "clientTlsKeyPath": "Path",
            "clientTlsCertificatePath": "Path",
            "clientKeyStorePassword": "String",
            "clientTrustStore": "Path",
            "clientTrustCertificates": [
              "Path"
            ],
            "clientTrustStorePassword": "String",
            "clientTrustMode": "TOFU",
            "knownClientsFile": "Path",
            "knownServersFile": "Path"
          },
          "communicationType": "REST",
          "properties": {
             "partyInfoInterval": "Long",
             "enclaveKeySyncInterval": "Long",
             "syncInterval": "Long",
             "resendWaitTime": "Long"
          }
        }
    ```

### Unix socket server configuration

=== "Unix socket"

    ```json
    {
        "app": "<app type",
        "enabled": <boolean,
        "serverAddress":"unix://[path]",
        "communicationType" : "REST"
    }
    ```

=== "Q2T Example"

    ```json
    {
        "app": "Q2T",
        "enabled": true,
        "serverAddress": "unix:/tmp/tm.ipc",
        "communicationType": "REST"
    }
    ```

### Configure CORS

The `ThirdParty` server type supports [configuring CORS] to control access to resources.

```json
{
    "app":"ThirdParty",
    "enabled": true,
    "serverAddress": "http://localhost:9081",
    "communicationType" : "REST",
    "cors" : {
        "allowedMethods" : ["GET", "POST", "PUT", "DELETE", "OPTIONS", "HEAD"],
        "allowedOrigins" : ["http://localhost:63342"],
        "allowedHeaders" : ["content-type"],
        "allowCredentials" : true
    }
}
```

[configuring CORS]: ../../Reference/SampleConfiguration.md#cors
