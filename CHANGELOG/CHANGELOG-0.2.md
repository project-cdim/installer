# Changelog 0.2

## [0.2.1](https://github.com/project-cdim/installer/compare/v0.2.0...v0.2.1) - 2026-10-09

The changes from v0.2.0 are as follows:

### Features

- Added the common configuration file `cdim.env` (template: `cdim.env.example`) for proxy, hostname, and port settings.
- Added generation of configuration files from `*.template` files using `cdim.env` when running `install --build`.
- Changed `post_install` to retrieve the public key from Keycloak and restart the gateway automatically.

### Breaking Changes

- `cdim.env` must be created before running `install --build`.

## [0.2.0](https://github.com/project-cdim/installer/compare/v0.1.1...v0.2.0) - 2026-03-24

The changes from v0.1.1 are as follows:

### Features

- Add mf-alert, layout-design-compose, and policy-manager-compose to the installation targets.
