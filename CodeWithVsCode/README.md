# 🛠️ C / C++ Setup Guide for VS Code (Windows)

This guide shows you, step by step, how to:

1. Install the **C/C++ compiler (GCC/G++)** using **MSYS2**
2. Install the **Code Runner** extension by **Jun Han** in VS Code
3. Configure Code Runner so your programs run inside the **VS Code terminal**

> 💻 This guide is for **Windows 10/11 (64-bit)**.

---

## ✅ What You Will Need

| Tool | Where to get it |
|------|-----------------|
| **VS Code** | https://code.visualstudio.com |
| **MSYS2** | https://www.msys2.org |
| **Code Runner** (extension) | Installed inside VS Code (Part 2) |

---

# Part 1 — Install the Compiler with MSYS2

## Step 1 — Download and install MSYS2

1. Go to **https://www.msys2.org**.
2. Click the download button for the **MSYS2 installer** (`msys2-x86_64-xxxxxxxx.exe`).
3. Run the installer.
4. Keep the default install location: **`C:\msys64`**
   > ⚠️ Don't change this path. The rest of this guide assumes `C:\msys64`. Avoid folders with spaces.
5. Click **Next** through the installer, then **Finish**.
6. Make sure **"Run MSYS2 now"** is checked when the installer finishes. A terminal window will open.

## Step 2 — Update MSYS2

In the MSYS2 terminal that opened, run:

```bash
pacman -Syu
```

- When asked `Proceed with installation? [Y/n]`, type `Y` and press **Enter**.
- The terminal may **close itself** after updating. That's normal.

Now open **MSYS2 UCRT64** from the Windows **Start Menu** (search "MSYS2 UCRT64") and run the update again:

```bash
pacman -Syu
```

> 📝 **Important:** Use the **UCRT64** terminal (the one with the yellow-ish icon), not "MSYS2 MSYS".

## Step 3 — Install the compiler toolchain

Still in the **MSYS2 UCRT64** terminal, run:

```bash
pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain
```

1. When asked to choose packages, just press **Enter** to accept the default (`all`).
2. When asked `Proceed with installation? [Y/n]`, type `Y` and press **Enter**.
3. Wait for the download and installation to finish. ☕ This can take a few minutes.

This installs **gcc** (C compiler), **g++** (C++ compiler), and **gdb** (debugger).

## Step 4 — Add the compiler to your Windows PATH

This lets VS Code (and any terminal) find `gcc` and `g++`.

1. Press the **Windows key** and search for **"Edit the system environment variables"**, then open it.
2. Click **Environment Variables...**
3. Under **User variables**, select **Path**, then click **Edit...**
4. Click **New** and paste:

   ```
   C:\msys64\ucrt64\bin
   ```

5. Click **OK** on all the windows to save.

## Step 5 — Verify the installation

1. **Close all** open terminals and VS Code windows. (This is required so the new PATH is loaded.)
2. Open **Command Prompt** or **PowerShell** (a fresh one).
3. Run these commands one at a time:

```bash
gcc --version
g++ --version
gdb --version
```

✅ If each command prints a version number, the compiler is installed correctly.

❌ If you see *"'gcc' is not recognized..."*, go back to **Step 4** and check that the path is exactly `C:\msys64\ucrt64\bin`, then restart your terminal.

---

# Part 2 — Install VS Code Extensions

## Step 6 — Install the Code Runner extension

1. Open **VS Code**.
2. Click the **Extensions** icon on the left sidebar (or press `Ctrl + Shift + X`).
3. In the search box, type **Code Runner**.
4. Find the one by **Jun Han** (publisher: `formulahendry`) and click **Install**.

   > ⚠️ Make sure the author is **Jun Han**. There are other extensions with similar names.

## Step 7 — (Recommended) Install the C/C++ extension

While you're in the Extensions panel:

1. Search for **C/C++**.
2. Install the one published by **Microsoft**.

This gives you code suggestions (IntelliSense), error highlighting, and debugging support.

---

# Part 3 — Configure Code Runner to Run in the VS Code Terminal

By default, Code Runner shows results in the **Output** panel, which **cannot accept keyboard input**, so `scanf()` and `cin` won't work there. We'll make it run in the **terminal** instead.

## Step 8 — Open your settings as JSON

1. Press `Ctrl + Shift + P` to open the Command Palette.
2. Type **Preferences: Open User Settings (JSON)** and press **Enter**.
3. A file called `settings.json` opens. You'll see something like:

```json
{
    "workbench.colorTheme": "Default Dark Modern"
}
```

## Step 9 — Paste the Code Runner configuration

Add the following **inside the curly braces `{ }`**. If there are already settings there, put a **comma `,`** after the last existing setting first.

```json
{
    "code-runner.runInTerminal": true,
    "code-runner.saveFileBeforeRun": true,
    "code-runner.clearPreviousOutput": true,
    "code-runner.executorMap": {
        "c": "cd $dir; gcc $fileName -o $fileNameWithoutExt; if ($?) { .\\$fileNameWithoutExt }",
        "cpp": "cd $dir; g++ $fileName -o $fileNameWithoutExt; if ($?) { .\\$fileNameWithoutExt }"
    }
}
```

Save the file with `Ctrl + S`.

### What each setting does

| Setting | Meaning |
|---------|---------|
| `runInTerminal` | Runs your program in the **VS Code terminal** so you can type input |
| `saveFileBeforeRun` | Auto-saves your file before running |
| `clearPreviousOutput` | Clears old output each time you run |
| `executorMap` (`c`, `cpp`) | The exact commands used to compile and run `.c` and `.cpp` files |

> 📝 **How the command works:** it moves into the file's folder, compiles with `gcc`/`g++`, and **only if compilation succeeds** (`if ($?)`), runs the compiled `.exe`.
>
> This version is written for the default **PowerShell** terminal in VS Code. It works on both old and new PowerShell versions.

---

# Part 4 — Test Your Setup

## Step 10 — Create a test folder and file

1. Create a folder for your code, e.g. `C:\Users\YourName\Documents\cpp-practice`
   > ⚠️ Avoid spaces and special characters in folder and file names (use `my-program.cpp`, not `my program.cpp`).
2. In VS Code: **File → Open Folder...** and choose that folder.
3. Create a new file called `hello.c` and paste:

```c
#include <stdio.h>

int main() {
    char name[50];
    printf("Enter your name: ");
    scanf("%49s", name);
    printf("Hello, %s! Your C setup works!\n", name);
    return 0;
}
```

4. Create another file called `hello.cpp` and paste:

```cpp
#include <iostream>
#include <string>
using namespace std;

int main() {
    string name;
    cout << "Enter your name: ";
    cin >> name;
    cout << "Hello, " << name << "! Your C++ setup works!" << endl;
    return 0;
}
```

## Step 11 — Run the code

Open `hello.c` or `hello.cpp`, then use any of these:

- Click the **▶ Run Code** button at the top-right corner of the editor
- Press **`Ctrl + Alt + N`**
- Right-click inside the editor → **Run Code**

The **terminal** opens at the bottom, asks for your name, and prints the greeting. 🎉

**To stop a running program:** press `Ctrl + Alt + M`, or click into the terminal and press `Ctrl + C`.

---

# 🔥 Troubleshooting

### `'gcc' is not recognized` / `gcc : The term 'gcc' is not recognized`
- The PATH isn't set correctly. Redo **Step 4**.
- **Close and reopen VS Code** completely after changing the PATH.

### The ▶ Run button doesn't appear
- Make sure Code Runner by **Jun Han** is installed and enabled.
- Make sure you've opened a `.c` or `.cpp` file.
- Restart VS Code.

### Output appears in the "Output" tab and I can't type input
- `"code-runner.runInTerminal": true` is missing from your `settings.json`. Redo **Step 9**.

### `Permission denied` or `cannot open output file ... .exe`
- The previous run of the program is **still running**. Stop it with `Ctrl + Alt + M`, or close the terminal and run again.

### `The token '&&' is not a valid statement separator`
- You're using the default Code Runner command in an older PowerShell. Use the `executorMap` from **Step 9**, which avoids `&&`.

### Compile errors with red text
- That's your code, not the setup! Read the error message. It tells you the **file name** and **line number** of the problem.

### Path has spaces and things break
- Move your project to a folder without spaces, e.g. `C:\code\cpp-practice`.

---

# 🧾 Quick Reference

| What you want to do | How |
|---------------------|-----|
| Run the current file | `Ctrl + Alt + N` or click ▶ |
| Stop the running program | `Ctrl + Alt + M` |
| Open the terminal | `` Ctrl + ` `` |
| Open the Command Palette | `Ctrl + Shift + P` |
| Check compiler is installed | `gcc --version` / `g++ --version` |
| Compile manually (C) | `gcc hello.c -o hello` then `.\hello` |
| Compile manually (C++) | `g++ hello.cpp -o hello` then `.\hello` |

---

# ✅ Setup Checklist

- [ ] MSYS2 installed in `C:\msys64`
- [ ] Ran `pacman -Syu` (twice) in MSYS2 UCRT64
- [ ] Installed the toolchain with `pacman -S --needed base-devel mingw-w64-ucrt-x86_64-toolchain`
- [ ] Added `C:\msys64\ucrt64\bin` to PATH
- [ ] `gcc --version` and `g++ --version` both work
- [ ] Code Runner by **Jun Han** installed
- [ ] Microsoft C/C++ extension installed
- [ ] Code Runner settings added to `settings.json`
- [ ] `hello.c` and `hello.cpp` both run in the terminal

Happy coding! 🚀
