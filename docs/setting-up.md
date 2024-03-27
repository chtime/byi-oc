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
5. Set up the runtime in a terminal (this will include *downloading about 5GB of data*), see [Using OpenShift Local](https://access.redhat.com/documentation/en-us/red_hat_openshift_local/2.33/html/getting_started_guide/using). It is also recommended to increase the allocated RAM before creating. 
    ```bash
    crc config set memory 16000
    crc setup
    ```

*Note: You may need to recreate the whole virtual machine if you decide to change these resources later.*

## Starting

To authenticate your cluster against Red Hats container registry, start it pointing at the pull secrets you obtained before:

```bash
crc start -p ~/Downloads/pull-secret
```

<details>
<summary>Troubleshooting Windows 🪟</summary>
#### ⚡Issue: Windows user not part of Hyper-V Administrators

To determine which users are members of the "Hyper-V Administrators" group, execute the following command:
```PowerShell
Get-LocalGroupMember -Group "Hyper-V Administrators"
```
To add the current user to this group, use the following command (Suggestions: restart the computer afterwards):
```PowerShell
([adsi]"WinNT://./Hyper-V Administrators,group").Add("WinNT://$env:UserDomain/$env:Username,user")
```

#### ⚡Issue: Port 80 is blocked
If this happens Branch Chaching needs to be disabled. This issue might arise even after applying Disable-BC and restarting the computer.
```PowerShell
Disable-BC
```

## Configuration

You may check or change configuration of cluster configuration params:

```bash
crc config view
```

```bash
crc config set consent-telemetry no
```

