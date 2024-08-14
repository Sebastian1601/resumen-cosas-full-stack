# Para iniciar la instalacion de programas y configuraciones para utilizar en una pc, lo primero es instalar Visual Studio, navegadores, y luego comenzar a instalar comandos de consola, como Winget.
Winget es parte de la "App Installer" de Microsoft Store.

```https://www.microsoft.com/p/app-installer/9nblggh4nns1#activetab=pivot:overviewtab```


luego de esto, ya podemos utilizar el comando de consola winget para instalar FNM (fast node manager) que nos permite instalar varias versiones de node en la pc, y correr los programas con ellas, sin tener que desinstalar una e instalar otra nueva.

## Instalar FNM.

https://github.com/Schniz/fnm?tab=readme-ov-file#shell-setup


## Comandos FNM. 

https://github.com/Schniz/fnm/blob/master/docs/commands.md


## Habilitar el comando fnm en el shell. 
Luego, para que fnm corra en cualquier shell que tengamos instalado(powershell, terminal, etc) debemos editar el perfil de windows de usuario. Normalmente existe y se puede abrir con el comando

`$profile`

si da un error al abrir el achivo, indicando que no se puede encontrar la ruta, debemos crear un archivo de perfil, de la siguiente manera:


## SOBRE PERFILES de windows:

You can create a PowerShell profile to customize your environment and add session-specific elements to every PowerShell session that you start.

A PowerShell profile is a script that runs when PowerShell starts. You can use the profile as a startup script to customize your environment. You can add commands, aliases, functions, variables, modules, PowerShell drives and more. You can also add other session-specific elements to your profile so they're available in every session without having to import or re-create them.

PowerShell supports several profiles for users and host programs. However, it doesn't create the profiles for you.
Profile types and locations


### Profiles locations

PowerShell supports several profile files that are scoped to users and PowerShell hosts. You can have any or all these profiles on your computer.

The PowerShell console supports the following basic profile files. These file paths are the default locations.

    All Users, All Hosts
        Windows - $PSHOME\Profile.ps1
        Linux - /opt/microsoft/powershell/7/profile.ps1
        macOS - /usr/local/microsoft/powershell/7/profile.ps1
    All Users, Current Host
        Windows - $PSHOME\Microsoft.PowerShell_profile.ps1
        Linux - /opt/microsoft/powershell/7/Microsoft.PowerShell_profile.ps1
        macOS - /usr/local/microsoft/powershell/7/Microsoft.PowerShell_profile.ps1
    Current User, All Hosts
        Windows - $HOME\Documents\PowerShell\Profile.ps1
        Linux - ~/.config/powershell/profile.ps1
        macOS - ~/.config/powershell/profile.ps1
    Current user, Current Host
        Windows - $HOME\Documents\PowerShell\Microsoft.PowerShell_profile.ps1
        Linux - ~/.config/powershell/Microsoft.PowerShell_profile.ps1
        macOS - ~/.config/powershell/Microsoft.PowerShell_profile.ps1

### How to create a profile

To create a PowerShell profile, use the following command format:
PowerShell

if (!(Test-Path -Path <profile-name>)) {
  New-Item -ItemType File -Path <profile-name> -Force
}

For example, to create a profile for the current user in the current PowerShell host application, use the following command:
PowerShell

if (!(Test-Path -Path $PROFILE)) {
  New-Item -ItemType File -Path $PROFILE -Force
}

In this command, the if statement prevents you from overwriting an existing profile. Replace the value of the $PROFILE variable with the path to the profile file that you want to create.


Luego de crear el perfil, se puede guardar info de shell utilizado, como asi habilitar funciones de comandos externos para utilizar en cualquier shell.
FNM indica cómo habilitar el propio.

Fuente:
https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_profiles?view=powershell-7.4


## Error : no se pudo cargar el perfil porque no está autorizado la ejecución de scripts en los perfiles de powershell --

Si luego de hacer todo esto, al abrir la consola se indica que no se cargó el perfil porque la ejecución de scripts está limitada, hay que realizar lo siguiente:

Long description

A script is a plain text file that contains one or more PowerShell commands. PowerShell scripts have a .ps1 file extension.

Running a script is a lot like running a cmdlet. You type the path and file name of the script and use parameters to submit data and set options. You can run scripts on your computer or in a remote session on a different computer.

Writing a script saves a command for later use and makes it easy to share with others. Most importantly, it lets you run the commands simply by typing the script path and the filename. Scripts can be as simple as a single command in a file or as extensive as a complex program.

Scripts have additional features, such as the #Requires special comment, the use of parameters, support for data sections, and digital signing for security. You can also write Help topics for scripts and for any functions in the script.


fuente:
https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-7.4

---

## Instalar versiones de nodejs mediante FNM.
Al tener habilitado el comando fnm de manera global, ya se puede utilizar fnm install y la versiòn de node que se quiera utilizar para correr programas en Visual Studio Code y desde cualquier Shell.

