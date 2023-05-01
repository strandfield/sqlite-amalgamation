
# SQLite

This repository contains a copy of SQLite amalgamation as can 
be downloaded on the [SQLite Download Page](https://www.sqlite.org/download.html#amalgtarball).

**Compiling**: see [How To Compile SQLite](https://www.sqlite.org/howtocompile.html).

**Building a Windows DLL**

I had some issue building a Windows DLL with the above documentation:
no `sqlite3.lib` file was produced.
It took me a while to figure out that no symbols were actually exported.

The solution, as suggested [here](https://www.purebasic.fr/english/viewtopic.php?t=72688) seems 
to be to manually define `SQLITE_API` to `__declspec(dllexport)`.

Solution: in the Visual Studio Command Prompt, run
```cmd
cl sqlite3.c -DSQLITE_API=__declspec(dllexport) -link -dll -out:sqlite3.dll
```

**See also**

[How to build static and dynamic libraries from .obj files for Visual C++?](https://stackoverflow.com/questions/31763558/how-to-build-static-and-dynamic-libraries-from-obj-files-for-visual-c)
