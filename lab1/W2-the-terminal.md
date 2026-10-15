# Coding Café - Lab 1
## The Terminal


**You will leave this lab with:** a `coding-cafe` folder built entirely from the terminal, your written
answers, and a log of every command you typed. All of it gets submitted. In Week 6 this same folder becomes
your first Git repository, so put it somewhere you will not delete.

> **There are 8 sections with 16 numbered questions in this sheet, and all of them get answered.**
> Your answers go in a file called `notes.md`, which you will create in section 2.
> Answer each one when you reach it.

**Rules of engagement**

- Type the commands. Do not paste them. The muscle memory is most of the point.
- Answer each question while its output is still on your screen.
- When something fails, read the message before you ask. It is a sentence in English.
- Stuck for more than five minutes? → ask a TA or the person next to you.

---

## 0 · Open a terminal

| | |
|---|---|
| macOS / Linux | Terminal app |
| Windows | WSL inside CMD |

Everyone should now see something ending in `$`. If yours ends in `%` you are on zsh - that is fine too,
everything below works identically.

---

## 1 · Where am I?

Run the following commands one at a time and observe the outputs:
```bash
pwd
ls
ls -a
ls -l
```

Add your answers to **Questions 1–3** in `notes.md` when you make it in the next section.

1. What did `pwd` print?
2. What did `ls -a` show that plain `ls` did not?
3. Pick one line from `ls -l`. What do you think the first column means?

**Checkpoint 1**

- [ ] `pwd`, `ls`, `ls -a` and `ls -l` have all run, and I know what each one told me.

---

## 2 · Build the folder

Make this exact structure, **using only the terminal**. No file explorer, no VS Code, no right-click → New Folder.

```bash
coding-cafe/
├── week01/
├── week02/
│   └── notes.md
└── README.md
```

Commands you need: `mkdir`, `cd`, `touch`, `ls`.

Do it from your home folder (`cd ~` gets you there).

**Then, without using `cd`:**

```bash
ls coding-cafe/week02
```

4. Why does that work from where you are standing? Which kind of path is `coding-cafe/week02`? Absolute or Relative?

> Add your answers to Q1-3 and all following questions to **`week02/notes.md`**. Keep it open beside your terminal for the rest of the lab.

**Checkpoint 2**

- [ ] `ls -R coding-cafe` shows the structure above, with nothing missing and nothing extra.
- [ ] `notes.md` is open, with answers to questions 1–4 in it.

---

## 3 · Move, copy, rename, delete

Still inside `coding-cafe` execute the following and observe the changes to your folder structure:

```bash
cp README.md README-backup.md
mv README-backup.md week01/
cd week01
mv README-backup.md old-readme.md
ls
```

5. `mv` did two different jobs above. What were they?

Now clean up:

```bash
rm old-readme.md
```

> ⚠️ There is no trash can. `rm` is permanent. Read the line twice before you press Enter.
> **Do not** run `rm -r` on anything today.

**Checkpoint 3**

- [ ] `week01` is empty again

---

## 4 · Where does the shell find things?

The shell keeps a short, ordered list of folders and stops at the first match (more info in the slides). Now look at yours.

```bash
echo $PATH
which python3
which pip
which ls
```

6. How many folders are on your `PATH`? (They are separated by `:`)
7. **Write down exactly where your `python3` lives.** You will need this again in a minute.
8. Compare your answer to 7 with the person next to you. Are they the same? If not, why might that be?

Now break something on purpose. Run the following (contains a deliberate typo):

```bash
pyton3
```

9. What exactly did the shell say? Explain the error in your own words, using the word **PATH**.

**Checkpoint 4**

- [ ] I have written down where my `python3` lives
- [ ] I can say what `command not found` means in terms of `PATH`

---

## 5 · A box of your own

In the session: your filesystem gets messy, versions collide, and the project that runs on your machine
does not run on anybody else's. The fix is to give each project its own box.

> If the following command fails with a message about `python3-venv` not being installed, **stop and call a TA**. It is a one-line fix, but it needs installing before you can go on.

```bash
cd ~/coding-cafe
python3 -m venv .venv
```

Then run the following:

```bash
ls
ls -a
```

10. `.venv` did not appear with plain `ls`. Why not? (Refer back to section 1.)

Now step into the box:

```bash
source .venv/bin/activate
```

After this you should see `(.venv)` at the beginning of your prompt.

> **If you are on Windows and not in WSL,** the command is different, because the folder layout inside a
> Windows venv is different - `Scripts\` instead of `bin/`:
>
> ```
> .venv\Scripts\Activate.ps1     PowerShell
> .venv\Scripts\activate.bat     CMD
> ```
>
> **A venv made in WSL will not work from Windows, and the reverse is also true.** A virtual environment
> stores the absolute path of the Python that built it, and WSL and Windows do not agree on what a path
> looks like. Activating the wrong one fails, or worse, quietly uses the wrong Python.
>
> If you end up working on the same project from both, build one in each and give them different names -
> `.venv` in WSL, `.venv-win` on Windows. Never copy a `.venv` folder from one to the other, and never
> put one in a shared or synced folder.
>
> For this course, work in **WSL only**.

11. What changed about your prompt?

And here is the point of the whole thing:

```bash
which python3
```

12. Compare this with what you wrote down for question 7. Is it the same path? If not, what does that tell
    you about what `activate` actually did to your `PATH`?

Now install something, but only inside the box:

```bash
pip list
pip install requests
pip list
```

13. What is in the second list that was not in the first?

Step back out:

```bash
deactivate
which python3
```

14. Where does `python3` point now?

**Checkpoint 5**

- [ ] `which python3` gives a different answer inside `.venv` than outside it
- [ ] `deactivate` has put my prompt back to normal

> **Note for Week 6:** `.venv` is a folder full of somebody else's code. It never goes into Git. You will
> tell Git to ignore it when we get there, for now just know it does not belong in a repository.

---

## 6 · Read a manual

The following command will open a sub-page inside your terminal. Scroll with the arrow keys. To go back to the terminal Quit with `q`.

```bash
man ls
```

15. Find what `ls -h` does. Write it in your own words.

Then, because it is a funny idea, open the manual for `man`:

```bash
man man
```

---

## 7 · Work faster

**Tab completion.** Type `cd cod` and press **Tab** before you finish. Then press Tab twice somewhere
ambiguous and see what it offers.

**History:** Press the **up arrow** a few times, you will see it scrolling through all your previous commands in order. Then run:

```bash
history
```

**Ctrl + C:** Start something that will not stop on its own:

```bash
python3
```

…and instead of `exit()`, press **Ctrl + C**, then **Ctrl + D**.

16. What is the difference between what Ctrl + C and Ctrl + D did?

---

## 8 · Finish your notes and submit

Check `week02/notes.md` has all **16** answers in it. Short answers - 2 to 3 sentences each, no more.
If you skipped any while you were working, go back and fill them in now.

Then, from inside `coding-cafe`, produce your command log:

```bash
history > week02/lab01-log.txt
```

> Look up what the `>` symbol just did.

That file is every command you typed today. You have just
used a tool to record your own work.

**Submit two things on Moodle:**

1. `week02/notes.md`
2. `week02/lab01-log.txt`

We will keep coming back to the `coding-cafe` folder for future labs.

---

## If it went wrong

| Message | What it usually means |
|---|---|
| `command not found` | Typo, or the program is not on your `PATH`. Run `which <program_name>` |
| `No such file or directory` | You are not where you think. Run `pwd` then `ls` |
| `No such file or directory: .venv/bin/activate` | You are in Windows, not WSL - or the venv was built by the other one. Build a fresh one where you are |
| `Permission denied` | You are trying to touch something that is not yours. Ask a TA |
| `python3-venv is not installed` | Call a TA - one-line fix |
| `(.venv)` is stuck on your prompt | Run `deactivate` |
| Terminal is stuck | `Ctrl + C`. If that fails, `Ctrl + D` |
| Something took over the screen | Press `q` |

---

## If you finished early

Explore the following:
- `ls -lh` - what changed, and why is that nicer?
- `cd -` a few times. What is it doing?
- `mkdir -p a/b/c/d` then `ls -R a`. What did `-p` save you from?
- Activate `.venv` again and run `pip freeze`. How is it different from `pip list`, and why might that
  format be more useful to somebody else?
- Look at `man grep`. No need to learn it yet. Just notice it exists - you will want it around Week 8.
