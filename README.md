# Resolving-mozjs

Official archive of the MozJS (SpiderMonkey)
https://archive.mozilla.org/pub/spidermonkey/releases/  
GoboLinux repository recipe: https://github.com/gobolinux/Recipes/tree/master/MozJS

Third party MozJS providers:  
https://salsa.debian.org/gnome-team/mozjs

polkit 0.114 requirements  
https://github.com/wingo/polkit/blob/master/NEWS

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
nano /Data/Compile/Recipes/MozJS/59.0a1.0/Recipe
Compile "MozJS" "24.2.0"
```
