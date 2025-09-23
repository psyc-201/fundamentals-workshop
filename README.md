# Fundamentals Workshop

Welcome to the fundamentals workshop! Our goals today are to:

- Get your laptop setup with R, Python, git/github, and any other tools you need to have a smooth experience when doing data analysis and participating in Grad-Stats (201 A/B)
- Get you familiar with tools and open-science workflows that you'll use throughout your scientific career
- Answer any technical questions and concerns you have

Don't worry if you have limited or no experience. Instead, focus on mastering the *core skills & intuitions* about programming, statistics, data-analysis, and inference and you'll be able to use *any* language.

## One time setup

While you might be familiar using apps in macOS via graphical-user-interfaces (GUIs) that you can point-and-click - building some core skills with the *command-line* will serve you well. 

You can interact with the command-line using the "Terminal" app (`cmd+spacebar` to open Spotlight and search for it). We'll use this to enter a few commands to get things setup. 

### 1. Homebrew

One of the core utilities you'll encounter frequently is [Homebrew](https://brew.sh). Think of is as the "app store" but for the command-line. Copy and paste the command below into your terminal to install it:

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

### 2. Git/Github

These tools allows us to keep our project under *version-control* and share it easily with others.  

1. Make sure you already have an existing [GitHub account](https://github.com/) and create one if not (use your edu email for extra free perks!)  
2. After logging-in, **create a [passkey](https://docs.github.com/en/authentication/authenticating-with-a-passkey/managing-your-passkeys#adding-a-passkey-to-your-account) for your account.** This will allow you to login into your account from your computer's terminal without entering a password.
3. Run the following command in your terminal: `brew install git gh`
4. Set your **local username to match your Github userid** and your **local email to match the [email you used on Github](https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-personal-account-on-github/managing-email-preferences/setting-your-commit-email-address?platform=mac#setting-your-commit-email-address-on-github)**:

- Configure your git username by running: `git config --global user.name "your-name"`  
- Configure your git email by running `git config --global user.email "your-email"`  
- Authenticate to github by running `gh auth login` and entering **the passkey you generated earlier**  

### 3. Pixi

Next, we'll use Homebrew to install [Pixi](#pixi), which will allow us to easily manage and install multiple versions of R and Python separately from each other:

```bash
brew install pixi
```

## Download a copy of this Repository

Now we're ready to create a copy of this project we can work with *locally* on our laptops:

### 1. Fork it to your account

This creates a copy of the repository under your *own* github account  


![](code/figures/CleanShot%202025-09-22%20at%2012.22.13.png)

### 2. Clone your fork

Then we'll "download" the repository to your local computer. First copy the URL using the screenshot:  

![](code/figures/CleanShot%202025-09-22%20at%2012.23.55.png)

Then pick a folder on your computer you want to download this to (you can use the `cd` command to change directories in the terminal and `pwd` to see where you are).  

Finally, use Github Desktop or your terminal to run: 

`git clone PASTE-URL-YOU-COPIED`

## Open the folder in VSCode

1. Open VSCode and use the account icon to login to your github acccount
2. Open the folder you cloned: File > Open 
3. You may get some pop-ups and warnings - **it's safe to accept them all** - these will configure VSCode with necessary extensions and tools to work with git, R, and Python!

Always remember: **The command-palette `cmd-shift-p` is your best friend!** 

When it doubt about how to do something, just serach for what you're trying to do and see what commands are available (change settings, color theme, open file, etc). 

We'll use that now to setup R & Python.

### Setup R & Python

Use the command-palette to search: "Terminal: Create New Terminal" 

Then run the following command:

```bash
pixi install
```

Followed by:

```bash
pixi run setup
```

### Render all project files

We can execute *all* the files in the project and open-up a live preview in our browsers by running:

```bash
pixi run render
```

### Working with R code

- Open `code/r-basics.qmd`
- Use the VScode command-palette to search: "Terminal: Create New Terminal"
- Start the R console by typing: `pixi run r`
- Then you can click any of the "Run cell" buttons above code

### Working with Python code

- Open `code/python-basics.qmd`
- Use the VScode command-palette to search: "Jupyter: Create Interactive Window"
- Then you can click any of the "Run cell" buttons above code

### Adding/Removing Libraries

- Use the commands below to add/remove Python and R libraries. They will be auto-update `pixi.toml`for you!
- Python: `pixi add package` or `pixi add --pypi package`
- R: `pixi add r-package`
- Removing: just swap `pixi add` with `pixi remove`

## Converting qmd and notebook files

- To work with files interactively *without* a separate preview window you may prefer the Jupyter notebook format (`.ipynb`)
- You can easily convert `.qmd` <-> `.ipynb` as both formats mix code + prose
  - However `.ipynb` files also store *outputs* (results, figures, etc)
- Just use `pixi run convert filename.qmd` or `pixi run convert filename.ipynb` and Quarto will convert to the other format

## Super Important

Despite what you read online when searching for R or Python help (or recieving help from AI):  
**Always prefer using `pixi add` and `pixi remove` instead of `install.packages()` in R or `pip install` / `conda install` in Python**  
This will save you from many unexpected headaches!

--- 

## Extra Details about the Tools

### How it Works

- The [Pixi](https://pixi.sh/latest/) package manager follows all instructions in `pixi.toml`
- The first `pixi install` you do will create a hidden `.pixi/` directory that includes an isolated Python/R installation with all specified packages
  - You don't need to version control this, it's very large! Only `pixi.toml` matters!
- We use pixi *commands* like `install`, `add`, `remove` install of working with Python or R package managers directly
  - This auto-updates `pixi.toml` for us!
- We interact with Quarto this way as well so that `.qmd` files always use the "right" R and Python (the ones in `.pixi` only)
  - `pixi run preview myfile.qmd`
- You can always "enter/activate" the environment if you need to do something via the command-line but need to use R/Python inside `.pixi/`
  - `pixi shell` -> environment is now active (like `conda activate myenv`)
- Similarily you can run arbitrary commands using packages in your environment
  - `pixi run quarto render myfile.qmd` -> Quarto version from environment is used to render file

### Pixi

A critical part of modern open-science workflows is *reproducibility.* It should be easy for anyone to be able rerun your code, with your data, and produce the same results and visualizations; this includes *future-you*! Throughout the course of your work you'll make use of a variety of R libraries and/or Python packages with specialized functionality (e.g. plotting, modeling, etc). To make our lives as easy as possible we'll use [Pixi](https://prefix.dev/blog/pixi_for_scientists) to handle all that stuff for us and more including:

- adding/removing R & Python libraries making sure they're compatible with other ones we're using
- running tasks/scripts we want to do repeatedly (e.g. run a pipeline)
- packing our own library/tool to share with others

There's only a few key pieces to understand when working with Pixi:

- `pixi.toml` - the human-readable "blueprints" file where Pixi tracks your dependencies and other info; **this is the most important** of the three
- `pixi.lock` - the less readable list of all currently installed libraries - what requested *and* what all those libraries depend on in turn - *you never need to touch this*
- `.pixi/` - a hidden folder that contains all the R & Python libraries and versions - *you never need to touch this*

If anything ever goes goes wrong you can *safely* delete `.pixi/` and `pixi.lock` and use `pixi install` to rebuild your setup from `pixi.toml`


#### Additional `pixi` commands

| Pixi Command | Description |
|--------------|-------------|
| `pixi install` | Creates a new environment and installs all dependencies |
| `pixi add pylib` / `pixi add r-lib` / `pixi add --pypi pylib` | Adds library to the environment |
| `pixi remove pylib` or `remove add r-lib` or `pixi remove --pypi pylib` | Removes library from the environment |
| `pixi run mytask` | Runs `mytask` task defined in the tasks section of `pixi.toml` |
| `pixi shell` | Activates the project environment in the current shell so you can use commands like `R`, `python`, `quarto` directly |

### Quarto

There are a variety of tools to perform *interactive* data-analysis in R and Python. You have already have encountered R-markdown or Jupyter Notebooks. [Quarto](https://quarto.org/docs/guide/) is a tool that can integrate and understand almost *all* these file-types and languages. This lets you combine the best parts of R tools (e.g. knitr documents) with Python tools (e.g. mixed code-cells and prose). You can use Quarto not only to work interactively with files, but create websites, blogs, books, and full manuscripts!

The files we've included here demonstrate examples of using R & Python to perform [**literate programming**](https://en.wikipedia.org/wiki/Literate_programming) - mixing English prose to explain & interpret from code. You can work with them in a few different ways:

- Run `pixi run render` to open a live preview of all `.qmd` files in the `code/` folder
- Use the command-palette in VSCode (`cmd+shift+p`) and select "Quarto: Preview" to open an auto-updating preview next to the file 
- Run `pixi preview myfile.qmd` in your terminal to open the same preview but in your browser
- Using `pixi run convert myfile.qmd` to produce a Jupyter Notebook file (`myfile.ipynb`) if you prefer that format instead; you can edit them in VSCode

