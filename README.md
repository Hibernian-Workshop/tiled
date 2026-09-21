Tiled Map Editor - https://www.mapeditor.org/

About Tiled
-------------------------------------------------------------------------------

Tiled is a general purpose tile map editor for all tile-based games, such as
RPGs, platformers or Breakout clones.

This Fork is for use in Hibernian Workshop projects.

How to contribute
-------------------------------------------------------------------------------

The original Tiled is developed in [Qt Creator](https://www.qt.io/development/tools/qt-creator-ide).

This fork is developed in VSCode. Therefore, it needs additional steps:

### 1. Install Qt

1. Create a [Qt Account](https://login.qt.io/register).
2. Download the [Qt Online Installer](https://www.qt.io/development/download-qt-installer-oss).
3. Log in with your account.
4. Keep the install folder `C:\Qt`.
5. Select **Custom installation**, and select these parts:
   - **Qt for Development → Qt → Qt 6.10.3 → MinGW 13.1.0 64-bit**
   - **Qt for Development → Qt → Qt 6.10.3 → Additional Libraries**
   - **Qt for Development → Qt → Build Tools → MinGW 13.1.0 64-bit**

The MinGW 13.1.0 tools include GCC and GDB.

### 2. Install and set up Qbs

You only need to do this step one time.

In PowerShell, run:

```powershell
Invoke-WebRequest https://download.qt.io/official_releases/qbs/3.1.1/qbs-windows-x86_64-3.1.1.zip -OutFile $env:TEMP\qbs.zip
Expand-Archive $env:TEMP\qbs.zip -DestinationPath C:\Qt\Tools\Qbs
Remove-Item $env:TEMP\qbs.zip
$env:PATH = "C:\Qt\Tools\Qbs\bin;$env:PATH"
qbs setup-toolchains C:\Qt\Tools\mingw1310_64\bin\x86_64-w64-mingw32-gcc.exe mingw
qbs setup-qt C:\Qt\6.10.3\mingw_64\bin\qmake.exe qt-tiled
qbs config profiles.qt-tiled.baseProfile mingw
qbs config defaultProfile qt-tiled
```

To check the result, run `qbs config --list profiles`. The list must show a `qt-tiled` profile.

### 3. Clone and open the repository

1. Clone the repository.
2. Open the repository folder in VSCode.
3. Install the recommended extensions.
4. Open the command palette and run **Qbs: Resolve**.

### 4. Build

1. In the status bar, select the `qt-tiled` profile and the configuration you want (**Debug** by default).
2. Open the command palette and run **Qbs: Build**.

### 5. Debug

Press `F5` and select **Debug Tiled (GDB)**.