# Coding Café - Lab 1 (Windows / PowerShell)
## The Terminal

> **Use this sheet only if you could not get WSL working.** Everything below does the same job as the main
> sheet, using PowerShell instead. Same 8 sections, same 16 questions, same submission.
>
> Talk to a TA about WSL when you get a chance. From Week 3 the labs are Python, which behaves the same
> either way, so you are not stuck — but Week 6 (Git) is easier with a Unix-style shell, and Git for Windows
> gives you one for free.

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

Press **Start**, type `PowerShell`, open **Windows PowerShell**.

You should see a prompt ending in `>`, something like `PS C:\Users\yourname>`.

> If you have **PowerShell 7** (black icon) or **Windows Terminal** installed, either is fine. Everything
> here works the same.

**One thing you need to know before we start.** PowerShell's real commands have long names like
`Get-ChildItem`. It also ships short nicknames — **aliases** — that match the Unix names, so `ls`, `cd`,
`cp`, `mv`, `rm` and `pwd` all work. We will use the short names. Where a flag differs from the Unix
version, it is called out.

---

## 1 · Where am I?

Run the following commands one at a time and observe the outputs:

```powershell
pwd
ls
ls -Force
```

> `ls -Force` is PowerShell's version of `ls -a`. PowerShell's plain `ls` already shows you what Unix needs
> `ls -l` for — look at the `Mode`, `Length` and `LastWriteTime` columns.

Add your answers to **Questions 1–3** in `notes.md` when you make it in the next section.

1. What did `pwd` print?
2. What did `ls -Force` show that plain `ls` did not?
3. Pick one line from `ls`. What do you think the `Mode` column means?

**Checkpoint 1**

- [ ] `pwd`, `ls` and `ls -Force` have all run, and I know what each one told me.

---

## 2 · Build the folder

Make this exact structure, **using only the terminal**. No File Explorer, no VS Code, no right-click → New.

```
coding-cafe\
├── week01\
├── week02\
│   └── notes.md
└── README.md
```

Commands you need: `mkdir`, `cd`, `ni`, `ls`.

> **PowerShell has no `touch`.** To make an empty file, use `ni` (short for `New-Item`):
>
> ```powershell
> ni README.md
> ```

Do it from your home folder (`cd ~` gets you there).

**Then, without using `cd`:**

```powershell
ls coding-cafe\week02
```

4. Why does that work from where you are standing? Which kind of path is `coding-cafe\week02`? Absolute or Relative?

> Add your answers to Q1-3 and all following questions to **`week02\notes.md`**. Keep it open beside your terminal for the rest of the lab.

**Checkpoint 2**

- [ ] `ls -Recurse coding-cafe` shows the structure above, with nothing missing and nothing extra.
- [ ] `notes.md` is open, with answers to questions 1–4 in it.

---

## 3 · Move, copy, rename, delete

Still inside `coding-cafe` execute the following and observe the changes to your folder structure:

```powershell
cp README.md README-backup.md
mv README-backup.md week01\
cd week01
mv README-backup.md old-readme.md
ls
```

5. `mv` did two different jobs above. What were they?

Now clean up:

```powershell
rm old-readme.md
```

> ⚠️ There is no Recycle Bin here. `rm` in PowerShell deletes permanently — it does **not** go to the bin
> the way deleting in File Explorer does. Read the line twice before you press Enter.
> **Do not** run `rm -Recurse` on anything today.

**Checkpoint 3**

- [ ] `week01` is empty again

---

## 4 · Where does the shell find things?

The shell keeps a short, ordered list of folders and stops at the first match (more info in the slides). Now look at yours.

```powershell
$env:Path
$env:Path -split ';'
Get-Command python
Get-Command pip
```

> Two differences from the slides. Windows separates the folders with a **semicolon** `;`, not a colon.
> And the command that answers "where does this live" is `Get-Command`, not `which`. The second line above
> splits the list so you can actually read it.

6. How many folders are on your `PATH`?
7. **Write down exactly where your `python` lives** — the `Source` column. You will need this again in a minute.
8. Compare your answer to 7 with the person next to you. Are they the same? If not, why might that be?

Now break something on purpose. Run the following (contains a deliberate typo):

```powershell
pyton
```

9. What exactly did the shell say? Explain the error in your own words, using the word **PATH**.

> **If `python` opened the Microsoft Store** instead of starting Python, that is Windows' placeholder, not
> a real Python. It means Python is not properly on your PATH. Call a TA.

**Checkpoint 4**

- [ ] I have written down where my `python` lives
- [ ] I can say what `is not recognized` means in terms of `PATH`

---

## 5 · A box of your own

In the session: your filesystem gets messy, versions collide, and the project that runs on your machine
does not run on anybody else's. The fix is to give each project its own box.

```powershell
cd ~\coding-cafe
python -m venv .venv
```

Then run the following:

```powershell
ls
ls -Force
```

10. `.venv` did not appear with plain `ls`. Why not? (Refer back to section 1.)

Now step into the box:

```powershell
.venv\Scripts\Activate.ps1
```

After this you should see `(.venv)` at the beginning of your prompt.

> ### ⚠️ If that failed with "running scripts is disabled on this system"
>
> This is the single most common thing to go wrong on Windows, and it is not your fault. Windows blocks
> PowerShell scripts by default. Run this once:
>
> ```powershell
> Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
> ```
>
> Answer `Y` when it asks. Then try `.venv\Scripts\Activate.ps1` again.
>
> `-Scope CurrentUser` means this only affects your account, not the whole machine, and you do not need
> administrator rights.

> **Note on the two worlds.** A venv built here stores the absolute path of the Python that made it. A venv
> made in WSL will not work from Windows, and the reverse is also true. If you later get WSL working, build
> a fresh one there — never copy a `.venv` folder between them, and never put one in OneDrive or any
> synced folder.

11. What changed about your prompt?

And here is the point of the whole thing:

```powershell
Get-Command python
```

12. Compare this with what you wrote down for question 7. Is it the same path? If not, what does that tell
    you about what `Activate.ps1` actually did to your `PATH`?

Now install something, but only inside the box:

```powershell
pip list
pip install requests
pip list
```

13. What is in the second list that was not in the first?

Step back out:

```powershell
deactivate
Get-Command python
```

14. Where does `python` point now?

**Checkpoint 5**

- [ ] `Get-Command python` gives a different answer inside `.venv` than outside it
- [ ] `deactivate` has put my prompt back to normal

> **Note for Week 6:** `.venv` is a folder full of somebody else's code. It never goes into Git. You will
> tell Git to ignore it when we get there, for now just know it does not belong in a repository.

---

## 6 · Read a manual

PowerShell's manual command is `help`. Run:

```powershell
help Get-ChildItem
```

Scroll with the arrow keys or spacebar. To go back to the terminal, quit with `q`.

> If it says the help files cannot be found, add `-Online` to open the same page in your browser instead:
> `help Get-ChildItem -Online`

15. Find what the `-Recurse` flag does. Write it in your own words.

Then, because it is a funny idea, open the manual for `help` itself:

```powershell
help help
```

---

## 7 · Work faster

**Tab completion.** Type `cd cod` and press **Tab** before you finish. Then press Tab twice somewhere
ambiguous and see what it offers.

**History:** Press the **up arrow** a few times, you will see it scrolling through all your previous commands in order. Then run:

```powershell
history
```

**Ctrl + C:** Start something that will not stop on its own:

```powershell
python
```

…and instead of `exit()`, press **Ctrl + C**, then **Ctrl + Z** followed by **Enter**.

> On Windows, the "end of input" key is **Ctrl + Z**, not Ctrl + D. Same idea, different key.

16. What is the difference between what Ctrl + C and Ctrl + Z did?

---

## 8 · Finish your notes and submit

Check `week02\notes.md` has all **16** answers in it. Short answers - 2 to 3 sentences each, no more.
If you skipped any while you were working, go back and fill them in now.

Then, from inside `coding-cafe`, produce your command log:

```powershell
history | Select-Object -ExpandProperty CommandLine > week02\lab01-log.txt
```

> Copy that line exactly. Plain `history > file` would give you a table with extra columns; the middle part
> pulls out just the commands. The `|` is a **pipe** — it sends the output of one command into the next.
> We will come back to it properly in a later week.

> Look up what the `>` symbol just did.

That file is every command you typed today. You have just
used a tool to record your own work.

**Submit two things on Moodle:**

1. `week02\notes.md`
2. `week02\lab01-log.txt`

We will keep coming back to the `coding-cafe` folder for future labs.

---

## If it went wrong

| Message | What it usually means |
|---|---|
| `is not recognized as the name of a cmdlet...` | Typo, or the program is not on your `PATH`. Run `Get-Command <program_name>` |
| `Cannot find path ... because it does not exist` | You are not where you think. Run `pwd` then `ls` |
| `running scripts is disabled on this system` | Execution policy. See the box in section 5 |
| `python` opens the Microsoft Store | Python is not properly installed or not on PATH. Call a TA |
| `Access to the path is denied` | You are trying to touch something that is not yours. Ask a TA |
| `(.venv)` is stuck on your prompt | Run `deactivate` |
| Terminal is stuck | `Ctrl + C`. If that fails, close the window |
| Something took over the screen | Press `q` |

---

## If you finished early

Explore the following:
- `ls -Recurse` inside `coding-cafe`. How is it different from plain `ls`?
- `mkdir a\b\c\d` then `ls -Recurse a`. Did it complain about the missing middle folders?
- Activate `.venv` again and run `pip freeze`. How is it different from `pip list`, and why might that
  format be more useful to somebody else?
- `Get-Command ls`. It does not give you a path like `Get-Command python` did. What does it give you
  instead, and what does that tell you about where `ls` actually comes from?
- Look at `help Select-String`. No need to learn it yet - it is Windows' version of a tool called `grep`,
  and you will want it around Week 8.
