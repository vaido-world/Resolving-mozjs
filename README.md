# Resolving-mozjs

Official archive of the MozJS (SpiderMonkey)
https://archive.mozilla.org/pub/spidermonkey/releases/  
GoboLinux repository recipe: https://github.com/gobolinux/Recipes/tree/master/MozJS

Third party MozJS providers:  
https://salsa.debian.org/gnome-team/mozjs

polkit 0.114 requirements  
https://github.com/wingo/polkit/blob/master/NEWS

If everything fails. The GVfs version can be reduced and these pre-compiled packages put on trial to resolve the needs of GVfs.
```
    InstallPackage "https://gobolinux.org/packages/016/Python--2.7.12-r1--x86_64.tar.bz2"
  InstallPackage "https://gobolinux.org/packages/016/MozJS--17.0.0-r2--x86_64.tar.bz2"
InstallPackage "https://gobolinux.org/packages/016/Polkit--0.112-r3--x86_64.tar.bz2"
```

### `Illegal instruction` error
This mostly happens on AMD processors.  
Trying to compile on an Intel processor is a way to go.  

### Research begins.
Python is required for the MozJS
Nano is used to prompt for necessary adjustments to the recipe.  
Suggested observations: Make sure configure is set as build tool.   
Suggested observations: Make sure dir contains `/js/src`  
if unsure check the: `/Data/Compile/Sources/` for extracted dir and make adjustments accordingly.  

```
InstallPackage "https://gobolinux.org/packages/016/Python--2.7.12-r1--x86_64.tar.bz2"
echo '\n' | MakeRecipe "MozJS" "24.2.0" "http://ftp.mozilla.org/pub/js/mozjs-24.2.0.tar.bz2"
nano /Data/Compile/Recipes/MozJS/24.2.0/Recipe
Compile "MozJS" "24.2.0"
```

#### Other versions
```
InstallPackage "https://gobolinux.org/packages/016/Python--2.7.12-r1--x86_64.tar.bz2"
echo '\n' | MakeRecipe "MozJS" "31.5.0" "https://archive.mozilla.org/pub/spidermonkey/releases/31.5.0/mozjs-31.5.0.tar.bz2"
nano /Data/Compile/Recipes/MozJS/31.5.0/Recipe
Compile "MozJS" "31.5.0"
```

### configure.py

`/js/src/configure` simply launches `/configure.py` with python. 

## polkit 
```
echo '\n' | MakeRecipe "Polkit" "0.114" http://www.freedesktop.org/software/polkit/releases/polkit-0.114.tar.gz
Compile "Polkit" "0.114"
```


## GVfs

```
InstallPackage --same "remove" "https://github.com/vaido-world/resolving-util-linux/raw/main/Util-Linux--2.35.1--x86_64.tar.bz2"

InstallPackage "https://gobolinux.org/packages/017/Fuse--2.9.7--x86_64.tar.bz2"
InstallPackage "https://gobolinux.org/packages/017/UnionFS-Fuse--2.1--x86_64.tar.bz2"

InstallPackage "https://github.com/vaido-world/Resolving-GLib/raw/main/GLib--2.68.4--x86_64.tar.bz2"




## GVfs Dependencies
#MakeRecipe "GSettings-Desktop-Schemas" "41" "https://gitlab.gnome.org/GNOME/gsettings-desktop-schemas/-/archive/master/gsettings-desktop-schemas-master.tar.bz2"
#Compile GSettings-Desktop-Schemas "41"
InstallPackage "https://github.com/vaido-world/Resolving-GLib/raw/main/GSettings-Desktop-Schemas/GSettings-Desktop-Schemas--41--x86_64.tar.bz2"

# Compile Gcr "3.12.0"
InstallPackage "https://github.com/vaido-world/Resolving-GVfs/raw/main/Gcr/Gcr--3.12.0--x86_64.tar.bz2"
nano /Data/Compile/Recipes/GVFS/1.48.1/Recipe
Compile "GVFS" "1.48.1"


```
