# Allow for case-insensitivity in Windows

Turn on Windows Feature - Windows Subsystem for Linux  
This allows you the option of having one folder called `learning` and another called `Learning` in the same directory. Not that I wanted this but I needed it as I'd messed up my git repo! 

You need to restart Windows and it will reboot a couple of times while it installs this feature. 

Once it's done, open command prompt in Admin mode and run

`fsutil.exe file SetCaseSensitiveInfo C:\folder\path enable`

You can set CaseSensitiveInfo on a specific folder, which is what I needed to do. 

Once it's enabled, I was about to `git clone` my repo and fix the mess. 

