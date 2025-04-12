# WSL and Docker Installation Guide
## WSL (Ubuntu) Installation

Begin by installing WSL with the default Ubuntu distro entering the following a command prompt:

```cmd
wsl --install
```

You may be asked to reboot, after rebooting, try launching default wsl distro:
```cmd
wsl
```

If it says you have no installed distributions, rerun the `wsl --install` command again.

On first run, create a user account and enter a password.

Next, exit out of the distro back to your command prompt using `exit`.

Verify that you have a WSL 2 distro using:
```cmd
wsl -l -v
```

Next, if you may want to move your distro to a different drive or location:

```
wsl --shutdown
wsl --manage Ubuntu --move G:\VM\WSL
```

If you want to see the location of your WSL distributions on disk, you can use `regedit` and look for BasePath in the subfolders of:
```
HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Lxss
```

At this point your WSL installation is ready to use and you can launch WSL again, either by using the Ubuntu icon in the start menu or by running the `wsl` command.

More information is available in the official [WSL installation guide](https://learn.microsoft.com/en-us/windows/wsl/install)

### Updating Ubuntu Dependencies

To update dependencies when using the default Ubuntu distribution, you may want to create a backup first in command prompt:
```
wsl --shutdown
wsl --export Ubuntu G:\VM\WSL\Ubuntu-Backup.tar
```

Next, use the following commands inside your WSL distro:
```
sudo apt get update
sudo apt get upgrade
```
