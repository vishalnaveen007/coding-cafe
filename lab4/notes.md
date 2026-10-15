# Lab 4 Notes

## Question 1
`--global` makes the setting apply to every Git repository for my user account on this computer, and it's stored in `~/.gitconfig`. Without it, Git would save the name and email only in the current repository's `.git/config`, so I'd have to set them again in every new repo.

## Question 2
`.git` is where Git keeps the repository's database: the commit history and objects, branch references, `HEAD`, and the repo's config. For example, `ls .git` showed `HEAD`, `config`, `objects`, `refs` and `hooks`.

## Question 3
Git offered to track about 5 top-level items: `.vscode/`, `lab1/`, `lab2/`, `lab3/` and `lab4/`, plus the files inside them. `.vscode/` is the one I didn't write myself, because VS Code created it for editor settings.

## Question 4
Nothing disappeared from my `git status`, because I had no `.venv/` folder to begin with. The only change was that `.gitignore` itself now appeared as untracked. 

## Question 5
`.gitignore` should be committed, not ignored. It is part of the project, and committing it means anyone who clones the repository gets the same ignore rules, so they don't accidentally add `.venv/` or other junk.

## Question 6
`README.md` moved from "Untracked files" to "Changes to be committed". In the three-places model, it went from the working directory to the staging area, ready to go into the next commit.

## Question 7
Git printed `[main (root-commit) dbe11fe] Lab work so far` and `8 files changed, 2574 insertions(+)`, followed by a line for each new file created. "root-commit" means it is the first commit in the repository.

## Question 8
The first seven characters (`dbe11fe`) are the short commit hash, an abbreviated form of the commit's full unique ID. It is used to refer to one exact commit, for example when inspecting it or going back to it.

## Question 9
The four steps of the loop are: edit a file, check what changed with `git status`, stage the change with `git add`, and save it into history with `git commit`.

## Question 10
`README.md` gets a special name and place because GitHub looks for a file with that name in the root of a repository and shows it, rendered as formatted text, on the front page. It's the first thing a visitor sees, so it explains what the project is and what it contains, unlike an ordinary notes file that nobody would open first.

## Question 11
`gh auth login` logged me in to GitHub through the browser and saved an access token on my computer. It also set up Git to use that token as its credential helper, so Git sends it automatically when I push and never asks me for a password.

## Question 12
The front page of the repository shows the contents of `README.md`, rendered as formatted text (heading, bold labels and the bullet list), below the list of files. GitHub does this because it automatically displays a README found in the root of a repository, as the project's introduction.

## Question 13
No, pushing did not change my local history. `git log --oneline` showed the same commits with the same hashes as before. Push only copies my commits to GitHub, and the only difference is that `origin/main` now appears next to my latest commit, showing that the remote is up to date.

## Question 14
A private repository exists on GitHub and holds all my files and history, but only I and the people I invite (here, the TAs) can see or access it. A repository that doesn't exist on GitHub has nothing stored there at all, so there is nothing to share and no off-site backup. Private means restricted access, while not existing means no copy online.5