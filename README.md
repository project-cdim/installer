# Installer

The pre-installer fetches the source from the Git repository, and the installer sets up the environment.
The post-installer configures the software after the installation is complete.

### Example Commands

Before running the installer, create `cdim.env` from `cdim.env.example` and edit it for your environment (proxy, hostname, and ports).
If editing the cloned .env file is necessary, do so before running the installer.

* To run the pre-installer, create `cdim.env`, edit the .env file, and run the installer (including starting the Docker container):
```
$ ./pre_install
$ cp cdim.env.example cdim.env
$ vi cdim.env
$ vi target_component_directory/.env
$ ./install --build --up
```

* To run the pre-installer, create `cdim.env`, edit the .env file, and run the installer (without starting the Docker container):
```
$ ./pre_install
$ cp cdim.env.example cdim.env
$ vi cdim.env
$ vi target_component_directory/.env
$ ./install --build
$ ./install --up
```

If editing the .env file is unnecessary, run the installer immediately after creating `cdim.env`.

* To run the pre-installer and then the installer (including starting the Docker container) without editing the .env file:
```
$ ./pre_install
$ cp cdim.env.example cdim.env
$ vi cdim.env
$ ./install --build --up
```

* Finally, to run the post-installer after running the installer (including starting the Docker container):
```
$ ./post_install
```

## Prerequisites for Using This Tool

* Assume that the source build is done with a Dockerfile.
* The user running the pre-installer, installer and post-installer should belong to the docker group or be the root user.
  * However, using the root user is not recommended.
* Environment-dependent files for each component should be stored in the "environment setup" Git repository, and source files should be stored in the "source" Git repository.
* Ensure that you can access Git.
* The following commands must be available: `envsubst` (used by the installer), `curl`, `jq`, and `openssl` (used by the post-installer).
* The pre-installer, installer and post-installer can be placed anywhere, but do not change the following structure:
```
<any directory>
  ├ pre_install (pre-installer)
  ├ pre_install.d/ (pre-installer extension directory)
  │   ├ extension scripts for individual environments
  │   └ config/
  ├ cdim.env.example (template of the common configuration file)
  ├ cdim.env (common configuration file, created from cdim.env.example)
  ├ install (installer)
  └ post_install (post-installer)
```

## pre_install

Function Overview
1. Clone from git
1. Execute extension scripts for individual environments if they exist

## install

Function Overview
1. Create the docker network [cdim-net]
1. Generate configuration files (such as `compose.yml`) from `*.template` files using the values in `cdim.env` (`--build` only)
1. Perform docker build with the pre-cloned files (`--build` only)
1. Start the docker container (`--up` only)
* If executed without arguments, the usage is displayed

## post_install
Function Overview
1. Retrieve the public key from Keycloak
1. Build and start the pre-cloned "set-up-tools" with Docker, and wait for it to finish
1. Restart the gateway in "base-compose" to apply the settings

## License

[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)
