# Installer

The pre-installer fetches the source from the Git repository, and the installer sets up the environment.

### Example Commands

If editing the cloned .env file is necessary, do so before running the installer.

* To run the pre-installer, edit the .env file, and run the installer (including starting the Docker container):
```
$ ./pre_install
$ vi target_component_directory/.env
$ ./install --up
```

* To run the pre-installer, edit the .env file, and run the installer (without starting the Docker container):
```
$ ./pre_install
$ vi target_component_directory/.env
$ ./install
$ docker compose up -d
```

If editing the .env file is unnecessary, run the installer immediately after the pre-installer.

* To run the pre-installer and then the installer (including starting the Docker container) without editing the .env file:
```
$ ./pre_install
$ ./install --up
```

* To run the pre-installer and then the installer (without starting the Docker container) without editing the .env file:
```
$ ./pre_install
$ ./install
$ docker compose up -d
```

## Prerequisites for Using This Tool

* Assume that the source build is done with a Dockerfile.
* The user running the pre-installer and installer should belong to the docker group or be the root user.
  * However, using the root user is not recommended.
* Environment-dependent files for each component should be stored in the "environment setup" Git repository, and source files should be stored in the "source" Git repository.
* Ensure that you can access Git.
* The pre-installer and installer can be placed anywhere, but do not change the following structure:
```
<any directory>
  ├ pre_install (pre-installer)
  ├ pre_install.d/ (pre-installer extension directory)
  │   ├ extension scripts for individual environments
  │   └ config/
  └ install (installer)
```

## pre_install

Function Overview
1. Clone from git
1. Execute extension scripts for individual environments if they exist

## install

Function Overview
1. Create the docker network [cdim_net]
1. Perform docker build with the pre-cloned files
1. Start the docker container based on the specified arguments
* If executed without arguments, only the build is performed, and the docker container must be started manually


## License

[Apache License 2.0](https://www.apache.org/licenses/LICENSE-2.0)
