# Setting up

In short, install [Red Hat OpenShift Local](https://developers.redhat.com/products/codeready-containers).

## System Prerequisites

- Any modern CPU, incl. Apple Silicon, with a few cores available
- ~10GB+ RAM
- 40GB+ storage

## Installation 

1. Get a Red Hat account
2. Download the installer in [RH's developer console](https://console.redhat.com/openshift/install/crc/installer-provisioned?intcmp=7013a000002CtetAAC)
3. Download the pull secrets just below, these will be used for authentication purposes later
4. Run the installer - *you will need elevated permissions for this!*
5. Set up the runtime in a terminal (this will include *downloading about 5GB of data*), see [Using OpenShift Local](https://access.redhat.com/documentation/en-us/red_hat_openshift_local/2.33/html/getting_started_guide/using)
    ```bash
    crc setup
    ```
6. 

## Starting

To authenticate your cluster against Red Hats container registry, start it pointing at the pull secrets you obtained before:

```bash
crc start -p ~/Downloads/pull-secret
```

## Configuration

You may check or change configuration of cluster configuration params:

```bash
crc config view
```

```bash
crc config set consent-telemetry no
```

