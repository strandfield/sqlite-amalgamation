
# SQLite

[![Build status](https://ci.appveyor.com/api/projects/status/3d9kt98y2bf9qrhy?svg=true)](https://ci.appveyor.com/project/strandfield/sqlite-amalgamation)

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

**AppVeyor Builds (Windows)**

| Branch        | Status    |
|---------------|-----------|
| current       | [![Build status](https://ci.appveyor.com/api/projects/status/3d9kt98y2bf9qrhy?svg=true)](https://ci.appveyor.com/project/strandfield/sqlite-amalgamation)     |
| **master**    | [![Build status](https://ci.appveyor.com/api/projects/status/3d9kt98y2bf9qrhy/branch/master?svg=true)](https://ci.appveyor.com/project/strandfield/sqlite-amalgamation/branch/master) |

The AppVeyor build has been configured to produce a Windows DLL and export it as artifact; 
a copy can therefore be downloaded [here](https://ci.appveyor.com/project/strandfield/sqlite-amalgamation/build/artifacts) from the latest build.

See `appveyor.yml` for more details.

**Building on Linux**

Using the sqlite3 dev package should work and be preferable.

```bash
sudo apt-get -y install libsqlite3-dev
```

But it is still possible to build the library manually by following the 
steps in tutorial linked above or the instructions in `README.txt`.

This repository defines a GitHub Workflow (see [C/C++ CI](https://github.com/strandfield/sqlite-amalgamation/actions/workflows/c-cpp.yml)) that builds SQLite by doing:

```bash
./configure
make
```

**See also**

[How to build static and dynamic libraries from .obj files for Visual C++?](https://stackoverflow.com/questions/31763558/how-to-build-static-and-dynamic-libraries-from-obj-files-for-visual-c)
