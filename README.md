# Fundamentals Workshop

- Cloning this repository and following the one-time setup steps below will give you a fully reproducible Python + R environment
- The key "blueprints" file that manages the environment, libraries, commands, etc is `pixi.toml`
- We can keep this file under version-control so that *anyone* can reproduce our setup using `pixi install`

## One time setup

1. [Install Homebrew](https://brew.sh/)
2. Install Pixi package manager: `brew install pixi` 
3. Clone this repository
3. Setup reproducible environment - from within the folder run `pixi install`
4. Configure Quarto - from with the folder run: `pixi run setup`
5. Open the folder with VSCode/Positron

## Executing Code

- Open any file in `code/` and run `pixi run preview filename.qmd` in your terminal
- The preview will auto-update whenever you save and cache expensive calculations

## Adding/Removing Libraries

- Use the commands below to add/remove Python and R libraries. They will be auto-update `pixi.toml`for you!
- Python: `pixi add package` or `pixi add --pypi package`
- R: `pixi add r-package`
- Removing: just swap `pixi add` with `pixi remove`

## Converting qmd and notebook files

- To work with files interactively *without* a separate preview window you may prefer the Jupyter notebook format (`.ipynb`)
- You can easily convert `.qmd` <-> `.ipynb` as both formats mix code + prose
  - However `.ipynb` files also store *outputs* (results, figures, etc)
- Just use `pixi run convert filename.qmd/ipynb` and Quarto will convert to the other format

## How it Works

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
