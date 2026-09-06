# CS0045 OpenGL Installation Guide

This guide explains how to install and configure **MSYS2**, the **GCC C++ compiler**, **FreeGLUT**, and **Visual Studio Code** for CS0045 activities.

> [!IMPORTANT]
> Complete each verification step before continuing to the next section.

---

## Table of Contents

1. system-requirements
2. install-msys2
3. update-msys2
4. install-the-gcc-c-compiler
5. verify-the-compiler-in-vs-code
6. install-freeglut
7. verify-freeglut
8. verify-freeglut-from-windows
9. add-the-msys2-terminal-to-vs-code
10. create-the-cs0045-workspace
11. setup-checklist

---

## 1. System Requirements

Before proceeding, make sure your computer meets the following requirements:

- A **64-bit Windows** computer
- **Windows 10 version 1809 or newer**
- Permission to install applications
- An internet connection
- **Visual Studio Code** installed

---

## 2. Install MSYS2

### Step 1: Download MSYS2

Visit the official MSYS2 website:

https://www.msys2.org/

Download the current **64-bit MSYS2 installer**.

### Step 2: Run the Installer

1. Open the downloaded installer.
2. Follow the installation instructions.
3. Use the following recommended installation location:

```text
C:\msys64
```

4. Complete the installation.
5. Allow the installer to launch the **MSYS2 UCRT64** environment.

> [!WARNING]
> For this course, always use **MSYS2 UCRT64**. Do not use the ordinary MSYS2 terminal for the compiler setup.

---

## 3. Update MSYS2

Open the following terminal from the Windows Start menu:

```text
MSYS2 UCRT64
```

Run the full system update command:

```bash
pacman -Syu
```

When asked whether you want to continue, enter:

```text
Y
```

### If the Terminal Asks You to Close It

MSYS2 may ask you to close the terminal after updating its core components.

If this happens:

1. Close the MSYS2 terminal.
2. Open **MSYS2 UCRT64** again.
3. Run the update command again:

```bash
pacman -Syu
```

> [!NOTE]
> MSYS2 is a rolling-release environment. Always complete the full system upgrade instead of updating only selected packages.

---

## 4. Install the GCC C++ Compiler

Inside the **MSYS2 UCRT64** terminal, run:

```bash
pacman -S mingw-w64-ucrt-x86_64-gcc
```

When prompted to continue, enter:

```text
Y
```

The package installs the GNU Compiler Collection, including support for:

- C
- C++
- OpenMP

### Verify the Installation

Run:

```bash
g++ --version
```

You should receive output similar to:

```text
g++.exe (Rev..., Built by MSYS2 project) 16.x.x
```

> [!NOTE]
> The exact GCC version may be different because MSYS2 packages are continuously updated.

---

## 5. Verify the Compiler in VS Code

Open **Visual Studio Code**, and then select:

```text
Terminal → New Terminal
```

In the PowerShell terminal, run:

```powershell
g++ --version
```

You should receive information about the installed GCC version.

Next, run:

```powershell
where.exe g++
```

The expected compiler location is:

```text
C:\msys64\ucrt64\bin\g++.exe
```

<img width="622" height="404" alt="{9673A222-D47B-4143-A7E1-F027406164BE}" src="https://github.com/user-attachments/assets/9dc41237-2ee7-4d9e-b0cd-c3914a2e03f3" />

> [!CAUTION]
> Do not continue until `g++` is detected in the VS Code terminal.

---

## 6. Install FreeGLUT

Return to the **MSYS2 UCRT64** terminal.

Run:

```bash
pacman -S mingw-w64-ucrt-x86_64-freeglut
```

When asked whether you want to continue, enter:

```text
Y
```

The FreeGLUT package provides the required header files, import libraries, and runtime DLL.

<img width="544" height="483" alt="{EEC8521A-BCB7-43DC-821F-9CF505913227}" src="https://github.com/user-attachments/assets/e1d43928-1a42-4584-b1d6-e5325a070163" />



Important installed files include:

```text
/ucrt64/include/GL/freeglut.h
/ucrt64/include/GL/glut.h
/ucrt64/lib/libfreeglut.dll.a
/ucrt64/bin/libfreeglut.dll
```

---

## 7. Verify FreeGLUT

In the **MSYS2 UCRT64** terminal, run each command separately.

### Check `freeglut.h`

```bash
ls /ucrt64/include/GL/freeglut.h
```

### Check `glut.h`

```bash
ls /ucrt64/include/GL/glut.h
```

### Check the FreeGLUT DLL

```bash
ls /ucrt64/bin/libfreeglut.dll
```

If all three files are displayed, FreeGLUT is installed correctly.

---

## 8. Verify FreeGLUT from Windows

Open the PowerShell terminal in Visual Studio Code.

### Check `freeglut.h`

```powershell
Test-Path C:\msys64\ucrt64\include\GL\freeglut.h
```

Expected result:

```text
True
```

### Check `glut.h`

```powershell
Test-Path C:\msys64\ucrt64\include\GL\glut.h
```

Expected result:

```text
True
```

### Check the FreeGLUT DLL

```powershell
Test-Path C:\msys64\ucrt64\bin\libfreeglut.dll
```

Expected result:

```text
True
```

<img width="530" height="139" alt="{460EF32A-97E8-49FB-A77D-D534E823FE1C}" src="https://github.com/user-attachments/assets/f7254083-ccc8-4d16-9ecb-d3c23f4b2cd4" />


> [!TIP]
> If PowerShell returns `False`, verify that MSYS2 was installed in `C:\msys64` and that the FreeGLUT installation completed successfully.

---

## 9. Add the MSYS2 Terminal to VS Code

You can add an **MSYS2 UCRT64** terminal profile to Visual Studio Code.

### Step 1: Open the Settings JSON File

In Visual Studio Code, press:

```text
Ctrl + Shift + P
```

Search for and select:

```text
Preferences: Open User Settings (JSON)
```

### Step 2: Add the Terminal Profile

Add the following configuration to the settings file:

```json
{
    "terminal.integrated.profiles.windows": {
        "MSYS2 UCRT64": {
            "path": "cmd.exe",
            "args": [
                "/c",
                "C:\\msys64\\msys2_shell.cmd",
                "-defterm",
                "-here",
                "-no-start",
                "-ucrt64"
            ]
        }
    }
}
```
<img width="762" height="632" alt="{8FE411FF-5077-4684-B1DF-0BB4BA5CF7A7}" src="https://github.com/user-attachments/assets/89e7922e-1dbd-47ad-9da2-876c4cc1a72e" />


> [!IMPORTANT]
> If your `settings.json` file already contains other settings, do not add another pair of outer `{ }` braces. Add only the `"terminal.integrated.profiles.windows"` property inside the existing JSON object, and make sure the properties are separated by commas.

### Step 3: Open the MSYS2 Terminal

In Visual Studio Code, select:

```text
Terminal → New Terminal → MSYS2 UCRT64
```

<img width="516" height="114" alt="{2140830F-32D7-4E37-A523-4DD50B3AE279}" src="https://github.com/user-attachments/assets/c049952b-ade7-472e-8a66-c712942e86be" />


You can now run MSYS2 UCRT64 commands directly inside Visual Studio Code.

---

## 10. Create the CS0045 Workspace

Create a folder in a convenient location, such as your **Documents** folder.

Recommended structure:

```text
Documents
└── CS0045
    └── SOURCE CODE
```

Open the workspace in Visual Studio Code:

1. Open **Visual Studio Code**.
2. Select **File → Open Folder**.
3. Navigate to the `CS0045` folder.
4. Select the `SOURCE CODE` folder.
5. Click **Select Folder**.

### Recommended Project Structure

```text
SOURCE CODE
│
├── .vscode
│   ├── c_cpp_properties.json
│   ├── tasks.json
│   └── launch.json
│
├── M3
├── M4
├── M5
├── M6
├── M7
├── M8
├── M9
├── M10
└── M11
```

## c_pp_properties.json
```json
{
    "configurations": [
        {
            "name": "MSYS2 UCRT64",
            "compilerPath": "C:\\msys64\\ucrt64\\bin\\g++.exe",
            "includePath": [
                "${workspaceFolder}/**",
                "C:\\msys64\\ucrt64\\include",
                "C:\\msys64\\ucrt64\\include\\GL"
            ],
            "defines": [
                "_DEBUG",
                "UNICODE",
                "_UNICODE"
            ],
            "cStandard": "c17",
            "cppStandard": "c++17",
            "intelliSenseMode": "windows-gcc-x64"
        }
    ],
    "version": 4
}
```

## launch.json
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Build and Debug Active C++ File",
            "type": "cppdbg",
            "request": "launch",
            "program": "${fileDirname}\\${fileBasenameNoExtension}.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${fileDirname}",
            "environment": [
                {
                    "name": "PATH",
                    "value": "C:\\msys64\\ucrt64\\bin;${env:PATH}"
                }
            ],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "C:\\msys64\\ucrt64\\bin\\gdb.exe",
            "setupCommands": [
                {
                    "description": "Enable GDB pretty-printing",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ],
            "preLaunchTask": "Build active C++ file with FreeGLUT"
        }
    ]
}
```

## tasks.json
```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Build active C++ file with FreeGLUT",
            "type": "shell",
            "command": "C:\\msys64\\ucrt64\\bin\\g++.exe",
            "args": [
                "-g",
                "-std=c++17",
                "${file}",
                "-o",
                "${fileDirname}\\${fileBasenameNoExtension}.exe",
                "-lfreeglut",
                "-lopengl32",
                "-lglu32"
            ],
            "options": {
                "cwd": "${fileDirname}"
            },
            "problemMatcher": [
                "$gcc"
            ],
            "group": {
                "kind": "build",
                "isDefault": true
            },
            "detail": "Compiles the currently active C++ file using MSYS2 UCRT64 GCC and FreeGLUT."
        }
    ]
}
```

> [!IMPORTANT]
> Create only one `.vscode` folder inside the main `SOURCE CODE` workspace. Do not create a separate `.vscode` folder inside every module.

The shared configuration can be used for all module folders.

---

## 11. Setup Checklist

Before starting your programming activities, verify the following:

- [ ] MSYS2 is installed in `C:\msys64`
- [ ] The MSYS2 system update completed successfully
- [ ] The GCC C++ compiler is installed
- [ ] `g++ --version` works in MSYS2 UCRT64
- [ ] `g++ --version` works in the VS Code terminal
- [ ] `where.exe g++` displays the correct UCRT64 compiler path
- [ ] FreeGLUT is installed
- [ ] The FreeGLUT header files exist
- [ ] `libfreeglut.dll` exists
- [ ] The MSYS2 UCRT64 terminal profile is available in VS Code
- [ ] The CS0045 workspace follows the recommended folder structure
- [ ] Only one `.vscode` folder is used for the entire workspace

---

## Expected Compiler Path

```text
C:\msys64\ucrt64\bin\g++.exe
```

## Expected FreeGLUT Files

```text
C:\msys64\ucrt64\include\GL\freeglut.h
C:\msys64\ucrt64\include\GL\glut.h
C:\msys64\ucrt64\bin\libfreeglut.dll
```

---

## Common Setup Issue

### The `g++` Command Is Not Recognized

If PowerShell cannot recognize the `g++` command:

1. Confirm that GCC was installed through **MSYS2 UCRT64**.
2. Run the following command in PowerShell:

```powershell
where.exe g++
```

3. Confirm that the compiler exists at:

```text
C:\msys64\ucrt64\bin\g++.exe
```

4. Restart Visual Studio Code after completing the installation.
5. Repeat the compiler verification commands.

> [!CAUTION]
> Do not begin the programming exercises until both GCC and FreeGLUT pass their verification checks.

---

## Reference

- [MSYS2 Official Website](https://www.msys2.org/)

---

**Course:** CS0045  
**Environment:** Windows, Visual Studio Code, MSYS2 UCRT64, GCC, and FreeGLUT
