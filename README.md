# Resolving-mozjs

Official archive of the MozJS (SpiderMonkey) https://archive.mozilla.org/pub/spidermonkey/releases/   
Current versions of MozJS https://ftp.mozilla.org/pub/firefox/releases/  
MozJS 52.0 version required by PolKit https://ftp.mozilla.org/pub/firefox/releases/52.0/source/   
 [js.tar.gz](https://github.com/vaido-world/Resolving-mozjs/files/7109752/js.tar.gz)

```
MakeRecipe https://ftp.mozilla.org/pub/firefox/releases/52.0/source/firefox-52.0.source.tar.xz
InstallPackage "https://gobolinux.org/packages/016/Python--2.7.12-r1--x86_64.tar.bz2"
```

```
root@LiveCD Compile/Sources/firefox-52.0/js/src]bash configure
zsh: illegal hardware instruction  bash configure
root@LiveCD Compile/Sources/firefox-52.0/js/src]bash
bash-5.0# bash configure
Illegal instruction
```

 
https://github.com/mozilla-spidermonkey/spidermonkey-embedding-examples/blob/esr78/docs/Building%20SpiderMonkey.md  

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
nano /Data/Compile/Recipes/Polkit/0.114/Recipe 
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

MakeRecipe "GVFS" "1.48.1" "https://gitlab.gnome.org/GNOME/gvfs/-/archive/master/gvfs-master.tar.bz2"
nano /Data/Compile/Recipes/GVFS/1.48.1/Recipe
Compile "GVFS" "1.48.1"


```
### nano GVfs Recipe

```
compile_version=017-GIT
url="https://gitlab.gnome.org/GNOME/gvfs/-/archive/master/gvfs-master.tar.bz2"
file_size=1419548
file_md5=63b79a71337b6b76c6d82b4b136d55e9
dir='gvfs-master'
recipe_type=meson
meson_variables=(
        "-Dsystemduserunitdir=no"
        "-Dtmpfilesdir=no"
 )
```


### maybe adding zlib might help
```
InstallPackage https://gobolinux.org/packages/016/ZLib--1.2.11-r1--x86_64.tar.bz2
```

Maybe the last time I installed mozjs externally without compiling
https://ubuntu.pkgs.org/18.04/ubuntu-main-amd64/libmozjs-52-dev_52.3.1-7fakesync1_amd64.deb.html


```
InstallPackage ThirdPartyInstallers --batch
curl "http://archive.ubuntu.com/ubuntu/pool/main/m/mozjs52/libmozjs-52-dev_52.3.1-7fakesync1_amd64.deb" -O
ThirdPartyInstaller "libmozjs-52-dev_52.3.1-7fakesync1_amd64.deb"
```



```
root@LiveCD LibMozjs-52-Dev/52.3.1_7fakesync1/lib/x86_64-linux-gnu/pkgconfig]ls
mozjs-52.pc

```


```
export PKG_CONFIG_PATH=LibMozjs-52-Dev/52.3.1_7fakesync1/lib/x86_64-linux-gnu/pkgconfig   

```



```
compile_version=017-GIT
url="http://www.freedesktop.org/software/polkit/releases/polkit-0.114.tar.gz"
file_size=1557340
file_md5=93ff41874e7df8c62ed9e41893817f04
dir='polkit-0.114'
recipe_type=configure
environment=(
   export PKG_CONFIG_PATH=/Programs/LibMozjs-52-Dev/52.3.1_7fakesync1/lib/x86_64-linux-gnu/pkgconfig:/Programs/LibElogind-Dev/239.3+20190131_1+debian1/lib/x86_64-linux-gnu/pkgconfig

)




```


```

checking for GLIB... yes
checking for LIBJS... yes
checking expat.h usability... yes
checking expat.h presence... yes
checking for expat.h... yes
checking for XML_ParserCreate in -lexpat... yes
checking for clearenv... yes
checking for fdatasync... yes
checking netgroup.h usability... no
checking netgroup.h presence... no
checking for netgroup.h... no
checking for LIBSYSTEMD... no
checking for LIBSYSTEMD_LOGIN... no
checking for LIBELOGIND... no
configure: error: Package requirements (libelogind) were not met:

No package 'libelogind' found

Consider adjusting the PKG_CONFIG_PATH environment variable if you
installed software in a non-standard prefix.

Alternatively, you may set the environment variables LIBELOGIND_CFLAGS
and LIBELOGIND_LIBS to avoid the need to call pkg-config.
See the pkg-config man page for more details.
PrepareProgram: configure failed.
Compile: Polkit 0.114 - Configuration failed.

```

```
ThirdPartyInstaller "http://ftp.us.debian.org/debian/pool/main/e/elogind/libelogind-dev_239.3+20190131-1+debian1_amd64.deb"
```


```
root@LiveCD ~]ld -lelogind --verbose
                          
ld: Attempt to open /lib/libelogind.so failed
ld: Attempt to open /lib/libelogind.a failed
ld: Attempt to open /usr/lib/libelogind.so failed
ld: Attempt to open /usr/lib/libelogind.a failed
ld: error: cannot find -lelogind
ld: Opened new descriptor 3 for "a.out"


```


```
ln -s  /Programs/LibElogind-Dev/239.3+20190131_1+debian1/lib/x86_64-linux-gnu/libelogind.so /usr/lib/elogind.so
```



```
SymlinkProgram /Programs/LibElogind-Dev
```


```

make[3]: Entering directory '/Data/Compile/Sources/polkit-0.114/src/polkit'
/Programs/Make/4.3/bin/make  all-am
make[4]: Entering directory '/Data/Compile/Sources/polkit-0.114/src/polkit'
  CCLD     libpolkit-gobject-1.la
/usr/bin/ld: error: cannot open /usr/lib/x86_64-linux-gnu/libelogind.so: No such file or directory
collect2: error: ld returned 1 exit status
make[4]: *** [Makefile:630: libpolkit-gobject-1.la] Error 1
make[4]: Leaving directory '/Data/Compile/Sources/polkit-0.114/src/polkit'
make[3]: *** [Makefile:560: all] Error 2
make[3]: Leaving directory '/Data/Compile/Sources/polkit-0.114/src/polkit'
make[2]: *** [Makefile:439: all-recursive] Error 1
make[2]: Leaving directory '/Data/Compile/Sources/polkit-0.114/src'
make[1]: *** [Makefile:499: all-recursive] Error 1
make[1]: Leaving directory '/Data/Compile/Sources/polkit-0.114'
make: *** [Makefile:431: all] Error 2
Compile: Polkit 0.114 - Build process failed.
```

```
root@LiveCD /usr/lib/x86_64-linux-gnu]ls
libelogind.so  pkgconfig

```

```
root@LiveCD /usr/lib/x86_64-linux-gnu]pwd
/usr/lib/x86_64-linux-gnu

```

libelogind.so is empty, of 0 bytes when using `l` command in the directory.

```
ThirdPartyInstaller http://ftp.us.debian.org/debian/pool/main/p/policykit-1/libpolkit-gobject-1-dev_0.105-31_amd64.deb
```

https://www.google.com/search?q=policykit&oq=policykit&aqs=chrome..69i57j69i60&sourceid=chrome&ie=UTF-8



https://launchpad.net/ubuntu/+source/mozjs78    

https://gitlab.freedesktop.org/polkit/polkit/-/blob/master/NEWS 

