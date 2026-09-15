# Dawarich

Self-hosted alternative to Google Location History

**This chart is not maintained by the upstream project and any issues with the chart should be raised
[here](https://github.com/alexvanderberkel/helm-charts/issues/new)**

## Source Code

* <https://github.com/Freika/dawarich>

## Dependencies

| Repository | Name     |
|----|----------|
| <https://dandydeveloper.github.io/charts> | redis-ha |

The chart deploys a PostGIS-backed PostgreSQL instance by default. To use an external PostgreSQL/PostGIS instance instead, set `postgresql.host` to your external database hostname and provide the external connection details (when `postgresql.host` is set, it is used even if `postgresql.enabled=true`). When using the bundled database with persistent storage, the initial database user and password are only applied when the database volume is first initialized. When using the bundled database, change `postgresql.auth.password` from its default or provide `postgresql.auth.existingSecret`.

## Installing the Chart

To install the chart with the release name `dawarich`

### OCI (Recommended)

```console
helm install dawarich oci://ghcr.io/alexvanderberkel/charts/dawarich
```

### Traditional

```console
helm repo add alexvanderberkel https://charts.esseling.photos
helm repo update
helm install dawarich alexvanderberkel/dawarich
```

## Values

Some of the most important values are documented below. Checkout the [values.yaml](./values.yaml) file for the complete documentation.

| Key                 | Type | Default | Description                                                                                                                                                                                                |
|---------------------|------|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| env                 | object | See [values.yaml](./values.yaml) | Environment variables used for configuration of Dawarich                                                                                                                                                   |
| dawarich            | object | See [values.yaml](./values.yaml) | Pod configuration for the Dawarich deployment                                                                                                                                                              |
| sidekiq             | object | See [values.yaml](./values.yaml) | Pod configuration for the Sidekiq deployment                                                                                                                                                               |
| image.pullPolicy    | string | `"IfNotPresent"` | Image pull policy                                                                                                                                                                                          |
| image.repository    | string | `"docker.io/freikin/dawarich"` | Image repository                                                                                                                                                                                           |
| ingress             | object | See [values.yaml](./values.yaml) | Enable and configure ingress settings for the chart under this key.                                                                                                                                        |
| persistence.export  | object | See [values.yaml](./values.yaml) | Configure watched volume settings for the chart under this key.                                                                                                                                            |
| persistence.public  | object | See [values.yaml](./values.yaml) | Configure public volume settings for the chart under this key.                                                                                                                                             |
| persistence.storage | object | See [values.yaml](./values.yaml) | Configure main storage volume settings for the chart under this key.                                                                                                                                       |
| postgresql          | object | See [values.yaml](./values.yaml) | Configure postgresql database subchart under this key. Dawarich will automatically be configured to use the credentials supplied to postgresql.                                                            |
| redis               | object | See [values.yaml](./values.yaml) | Configure redis subchart under this key. Dawarich will automatically be configured to use the credentials supplied to redis. [[ref]](https://github.com/DandyDeveloper/charts/tree/master/charts/redis-ha) |

To use an external Redis instance, set `.enabled: false` with the external host and port. E.g. for external Redis;

```yaml
redis:
  enabled: false
  host: my.redis.cluster
  port: 6379

  # existingSecret: provide your own secret
  redisPassword: changeme
```