# phun-services

Builds of services that [Phun](https://github.com/cloudcake/phun) installs but
whose projects publish no build for some platforms. Each workflow builds one
service from its upstream source, checks that it starts and answers, and
publishes the archives with a `SHA256SUMS` on a release tagged
`<service>-<version>`. Phun pins those checksums in `resources/downloads.json`
with `scripts/pin-services.sh <tag>`.

| Workflow | Platforms | Why |
|---|---|---|
| `valkey-build` | macOS (Apple Silicon, Intel) | Valkey publishes Linux tarballs only |
| `mariadb-build` | macOS (Apple Silicon, Intel) | MariaDB publishes Linux and Windows only |
| `memcached-build` | Linux (x86_64, aarch64), macOS (Apple Silicon, Intel) | memcached.org publishes source only |

All workflows are manual (`workflow_dispatch`): run them from the Actions tab.
Each one refuses to replace an existing release; delete it first to rebuild.
The archives keep each project's own licence: Valkey and memcached are
BSD-3-Clause, MariaDB is GPL-2.0.
