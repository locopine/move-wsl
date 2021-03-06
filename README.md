# Move WSL

Bash, batch and PowerShell script to move WSL 1 and WSL 2 distros VHDX file to a different location.

![Interactive Example](screencast.gif)

## Usage

### Bash
Use with git bash for Windows or similiar.

#### Interactive way
1) `./move-wsl`
2) Select your distro
3) Enter your target (i.e. `/d/wsl target/ubuntu`)

#### Explicit way
1) Get a list of WSL distros: `wsl -l`
2) Move your image: `./move-wsl [NAME] [LOCATION]`

__Example:__ `./move-wsl docker-desktop /d/docker`


### PowerShell
Interactive way of moving wsl for Windows PowerShell.

1) `./move-wsl.ps1`
2) Select your distro
3) Enter your target (i.e. `D:\wsl target\ubuntu`)

### Batch
_This is a lightweight version_ which can also be used from Windows CMD.

1) Get a list of WSL distros: `wsl -l`
2) Move your image: `move-wsl.bat [NAME] [LOCATION]`

__Example:__ `move-wsl.bat docker-desktop "D:\wsl files\docker"`

## Moving Docker WSL

Before moving Docker WSL make sure to stop the Docker service. Otherwise Docker will crash and you may need to reset it to factory defaults.

## FAQ

### Default user was switched to root when moving a distro

Set your default user inside your distro by adding the following configuration to your `/etc/wsl.conf`.

```ini
[user]
default=YOUR_USERNAME
```

If the file doesn't exist create it manually. Then exit your distro, terminate it (`wsl -t YOUR_DISTRO`) and start it again. For further options see [Microsoft Docs](https://docs.microsoft.com/en-us/windows/wsl/wsl-config#user).

### Standard distro switched when moving it

Since we need to unregister to import it with the same name, the standard distro can be switched. Just set your standard distro again:

```sh
wsl -s YOUR_DISTRO
```

### WSL version was switched when moving distro

On import the distro will be registered with the current default WSL version. You can set your default WSL version with `wsl --set-default-version <Version>`.
When the WSL version was accidentally changed while moving, you can set the version with `wsl --set-version <Distro> <Version>`.

## Changelog

### 1.3.1 - 2020-08-09
Fix: Bug in Batch script not validating export properly when using a path with spaces.

### 1.3.0 - 2020-07-16
Feat: WSL1 support.

### 1.2.2 - 2020-07-16
Fix: Error in PowerShell script when only one distro is installed Better error handling of export by [manie204](https://github.com/manie204).

### 1.2.1 - 2020-07-07
Feat: Better error handling of export by [Schop0](https://github.com/Schop0). \
Fix: Replace newlines in wsl command output as it broke selection sometimes.

### 1.2.0 - 2020-06-23
Feat: Added PowerShell version by [sidecus](https://github.com/sidecus).

### 1.1.2 - 2020-06-22
Change: Use `-q` query for more parseble output of distros.

### 1.1.1 - 2020-05-29
Fix: (Default) appendix was breaking distro selection in interactive mode.

### 1.1 - 2020-04-14
Feat: Add interactive mode for bash script.

### 1.0 - 2020-04-13
Feat: Add validation for successfull export and import for bash and batch script.
