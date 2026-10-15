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