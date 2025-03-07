# auth0-exporter

The helm chart for the auth0 prometheus exporter.

[![Version](https://img.shields.io/github/v/release/tfadeyi/auth0-simple-exporter?color=blue&label=Version&sort=semver&style=flat-square)](https://img.shields.io/github/v/release/tfadeyi/auth0-simple-exporter?color=blue&label=Version&sort=semver&style=flat-square)
![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square)
[![AppVersion](https://img.shields.io/github/v/release/tfadeyi/auth0-simple-exporter?color=blue&label=AppVersion&sort=semver&style=flat-square)](https://img.shields.io/github/v/release/tfadeyi/auth0-simple-exporter?color=blue&label=AppVersion&sort=semver&style=flat-square)

## Additional Information

The Auth0 exporter helm chart installs the exporter on the target cluster, the collected metrics will exposed
on the `/metrics` endpoint.

## Installing the Chart

### Deploying the chart

#### Pass secret to chart as a value, it creates the secret
    This shows a simple installation of the exporter helm chart, running with TLS disabled.
    ```shell
    export TOKEN="< auth0 management API static static token >"
    export DOMAIN="< auth0 tenant domain >"
    ```
    ```shell
    # Installing by passing in secret directly
    helm repo add auth0-exporter https://tfadeyi.github.io/auth0-simple-exporter
    helm upgrade --install --create-namespace -n auth0-exporter auth0-exporter/auth0-exporter \
      --set auth0.domain="$DOMAIN" --set auth0.token="$TOKEN" \
      --set exporter.tls.disabled=true
    ```

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| auth0 | object | `{"clientId":"","clientSecret":"","createSecret":true,"domain":"<change_me>.eu.auth0.com","secretName":"auth0-credentials","token":""}` | Exporter's Auth0 client configuration |
| auth0.clientId | string | `""` | Auth0 management api client-id. (do not set if static token is already set) |
| auth0.clientSecret | string | `""` | Auth0 management api client-secret. (do not set if static token is already set) |
| auth0.domain | string | `"<change_me>.eu.auth0.com"` | Auth0 tenant's domain. (i.e: <tenant_name>.eu.auth0.com) |
| auth0.token | string | `""` | Auth0 management api static token. (the token can be used instead of client credentials) |
| exporter | object | `{"logLevel":"info","metricsEndpoint":"metrics","namespace":"","port":9301,"pprof":false,"tls":{"auto":false,"certFile":"","createSecret":false,"disabled":false,"hosts":[],"keyFile":"","secretKey":"","secretName":""}}` | Exporter's configuration |
| exporter.metricsEndpoint | string | `"metrics"` | URL Path under which to expose the collected auth0 metrics. |
| exporter.port | int | `9301` | Port where the server will listen. |
| exporter.pprof | bool | `false` | Enabled pprof profiling on the exporter on port :6060. (help: https://jvns.ca/blog/2017/09/24/profiling-go-with-pprof/) |
| exporter.tls | object | `{"auto":false,"certFile":"","createSecret":false,"disabled":false,"hosts":[],"keyFile":"","secretKey":"","secretName":""}` | Exporter's TLS configuration |
| exporter.tls.auto | bool | `false` | Allow the exporter to use autocert to renew its certificates with letsencrypt. (can only be used if the exporter is publicly accessible by the internet) |
| exporter.tls.certFile | string | `""` | The certificate file for the exporter TLS connection. |
| exporter.tls.disabled | bool | `false` | Run exporter without TLS. |
| exporter.tls.keyFile | string | `""` | The key file for the exporter TLS connection. |
| fullnameOverride | string | `""` | Helm default setting, use this to shorten install name |
| image | object | `{"pullPolicy":"IfNotPresent","repository":"ghcr.io/tfadeyi/auth0-simple-exporter","tag":"v0.1.1"}` | image settings |
| imagePullSecrets | list | `[]` | specify credentials if pulling from a customer registry |
| labels | object | `{}` |  |
| nameOverride | string | `""` | Helm default setting to override release name, leave blank |
| nodeSelector | object | `{}` |  |
| podAnnotations | object | `{}` |  |
| podSecurityContext | object | `{}` |  |
| replicaCount | int | `1` |  |
| resources.limits.cpu | string | `"100m"` |  |
| resources.limits.memory | string | `"128Mi"` |  |
| resources.requests.cpu | string | `"100m"` |  |
| resources.requests.memory | string | `"128Mi"` |  |
| securityContext.capabilities.drop[0] | string | `"ALL"` |  |
| securityContext.readOnlyRootFilesystem | bool | `true` |  |
| securityContext.runAsNonRoot | bool | `true` |  |
| securityContext.runAsUser | int | `1000` |  |
| service.port | int | `9301` |  |
| service.type | string | `"ClusterIP"` |  |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created |
| serviceAccount.name | string | `""` |  |
| tolerations | list | `[]` |  |

----------------------------------------------
Autogenerated from chart metadata using [helm-docs v1.11.2](https://github.com/norwoodj/helm-docs/releases/v1.11.2)
