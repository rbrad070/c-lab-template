# CPSC 100 Coursework

This is your personal workspace for CPSC 100 (Introduction to Programming in C) at Selkirk College. Use it for your tutorial questions and assignments.

Open this repo in **GitHub Codespaces** (**<> Code** → **Codespaces**) to get a ready-to-use C environment in your browser, with `gcc`, `gdb`, `make`, and `valgrind` already installed. You don't need to install anything on your own computer.

For full setup and submission instructions, see the **Codespaces Setup Guide** on the course Moodle page.

## Folders

- `tutorials/`: tutorial questions, one folder each (e.g. `tutorials/tut03`)
- `assignments/`: assignments, one folder each (e.g. `assignments/a1`)

## Using the terminal: a quick primer

The **terminal** is the panel at the bottom of the Codespace where you type commands. If it isn't showing, open it from the menu ☰ → **Terminal** → **New Terminal**.

### The prompt tells you where you are

The terminal is always "in" one folder, called the **current directory**. The prompt shows which one:

```
@jsmith ➜ /workspaces/cpsc100-work/tutorials (main) $
```

This means you're in the `tutorials` folder inside your repo. Every command you type runs in that folder.

Your repo lives at `/workspaces/cpsc100-work`. That's the top of your repo, where `tutorials/` and `assignments/` are.

### Commands for moving around

| Command | What it does |
|---|---|
| `pwd` | **P**rint **w**orking **d**irectory: show the folder you're in |
| `ls` | **L**i**s**t the files and folders in the current folder |
| `cd tutorials` | **C**hange **d**irectory: go into the `tutorials` folder |
| `cd tutorials/tut03` | Go down two levels at once |
| `cd ..` | Go **up** one folder (to the parent folder) |
| `cd /workspaces/cpsc100-work` | Jump straight back to the top of your repo |

A folder path uses `/` to separate folder names: `tutorials/tut03` means "the `tut03` folder inside `tutorials`".

### Shortcuts that save typing

| Key | What it does |
|---|---|
| **Tab** | Auto-complete a file or folder name. Type `cd tu` then press Tab, and it fills in `tutorials/` |
| **↑** (up arrow) | Bring back your previous command. Keep pressing to go further back |
| **Ctrl + C** | Stop a program that's stuck or running forever |
| `clear` | Clear the terminal screen |

**Don't use spaces in file or folder names.** Use `tut-03` or `tut_03`, not `tut 03`. Spaces make terminal commands break in confusing ways.

## Compiling and running

`gcc` only looks for your `.c` file **in the current directory**. Before you compile, you must be in the folder that contains your source file.

### Step 1: Get to the right folder

**Easiest way:** in the Explorer on the left, right-click the folder that holds your `.c` file → **Open in Integrated Terminal**. The new terminal starts in that folder.

**Or use `cd`.** For example, to get from the top of your repo to `tutorials/tut03`:

```bash
@jsmith ➜ /workspaces/cpsc100-work (main) $ cd tutorials/tut03
@jsmith ➜ /workspaces/cpsc100-work/tutorials/tut03 (main) $
```

### Step 2: Check you're in the right place

Look at the prompt, then run `ls`. Your `.c` file must be in the list:

```bash
@jsmith ➜ /workspaces/cpsc100-work/tutorials/tut03 (main) $ ls
hello.c
```

If you don't see your file, you're in the wrong folder. Use `cd ..` to go up, `ls` to look around, and `cd` into the right folder.

### Step 3: Compile

```bash
gcc -Wall -Wextra -std=c11 -g hello.c -o hello
```

| Part | What it means |
|---|---|
| `-Wall -Wextra` | Show warnings about likely mistakes. Read them and fix them |
| `-std=c11` | Use the C11 version of the C language |
| `-g` | Include information for the debugger |
| `hello.c` | Your source file |
| `-o hello` | Name the finished program `hello` |

No output means it compiled cleanly. If there are errors, fix your code, save (**Ctrl + S**), and compile again. Press **↑** to bring the gcc command back instead of retyping it.

### Step 4: Run

```bash
./hello
```

`./` means "the program in this folder".

### Common problems

| Message | What's wrong |
|---|---|
| `gcc: error: hello.c: No such file or directory` | You're in the wrong folder, or the file name is spelled differently. Run `pwd` and `ls` to check. |
| `bash: ./hello: No such file or directory` | The program wasn't built. Scroll up for gcc errors, fix them, and compile again. |
| `bash: cd: tut03: No such file or directory` | That folder isn't inside the one you're in. Run `ls` to see which folders are here. |
| Your changes don't show up when you run the program | You forgot to save or to recompile. Save, run gcc again, then run the program. |

## Your first task: run the welcome programs

There's a `welcome.c` in **both** the `tutorials` folder and the `assignments` folder. Compile and run each one to check that everything works and to practise moving between folders.

**1. The tutorials welcome.** Right-click the `tutorials` folder → **Open in Integrated Terminal**, then:

```bash
ls                                               # you should see welcome.c
gcc -Wall -Wextra -std=c11 -g welcome.c -o welcome
./welcome
```

**2. The assignments welcome.** This time, move there with `cd` from the same terminal:

```bash
cd ..                                            # up to the top of your repo
cd assignments                                   # into the assignments folder
pwd                                              # should end in /assignments
ls                                               # you should see welcome.c
gcc -Wall -Wextra -std=c11 -g welcome.c -o welcome
./welcome
```

Both files are called `welcome.c`, but each program prints something different. **gcc compiles the file in the folder your terminal is in**, so always check where you are before you compile.

**3. Make it yours.** Open `tutorials/welcome.c`. In the comment at the top, change `Student: YOUR NAME HERE` to your name, and save with **Ctrl + S**.

**4. Save your work to GitHub.** Commit and sync (Source Control → type `Added my name to welcome.c` → **✓ Commit** → **Sync Changes**). Then check your repo on github.com to see your commit.

Notice that Source Control lists only `welcome.c`, not the `welcome` programs you compiled. That's the `.gitignore` file at work (see [The `.gitignore` file](#the-gitignore-file)).

If both programs printed their welcome messages, you're ready for Tutorial 1.

## Important

- **Do not edit or delete the `.devcontainer` folder.** It sets up your coding environment and turns off autocomplete and AI assistants for this course.
- **Do not edit or delete the `.gitignore` file.** See [The `.gitignore` file](#the-gitignore-file) below.
- **Commit and sync your work often.** Codespaces that go unused for 30 days are deleted, and any work that isn't committed is lost.

## The `.gitignore` file

Your repo has a file called `.gitignore`. It tells Git which files **not** to save to GitHub when you commit.

When you compile, gcc creates a program file (like `welcome` or `hello`) next to your `.c` file. That program is built from your code, so there's no need to save it. You can always rebuild it by compiling again. `.gitignore` makes Git skip those program files and other build leftovers, so your commits contain only the code you wrote.

This means:

- **Source Control only lists your `.c` files and other real work**, not the programs you've compiled.
- **Your repo stays small and tidy**, and downloads from GitHub contain only your code.
- **Compiled programs still stay in your Codespace.** They just aren't saved to GitHub.

**Do not edit or delete `.gitignore`.** Without it, every program you compile gets added to your commits.

> Files whose names start with a dot, like `.gitignore` and `.devcontainer`, are *hidden* files. They're normal, and they show up in the Codespace Explorer. `ls` doesn't show them, but `ls -a` does.