# plockalyser

*"package lock analyser"*

Utility for performing rudimentary analysis on npm package dependencies from an
npm lock file.

## Prepare data

Get data from `package-lock.json` in your project:

```shell
npm ls --all --json > npm_ls.json
```

or if you want to exclude the dev dependencies:

```shell
npm ls --all --omit-dev --json > npm_ls_nodev.json
```

Copy the file to the `plockalyser` directory.

## Running

### Bootstrap

`plockalyser` uses [uv](https://github.com/astral-sh/uv) for managing
dependencies; it can be installed e.g. with `pipx install uv`. Regular `pip`
might also work, but YMMV.

Setting up:

```shell
uv sync
```

Command line arguments:
```shell
./plockalyser.py --help
```

Produce Markdown tables with some basic data, output to stdout:
```shell
./plockalyser.py npm_ls.json --tables
```

The tables are suitable for processing with [Pandoc](https://pandoc.org/), and
are marked up for inclusion using the
[pandoc-include](https://github.com/DCsunset/pandoc-include) filter (optional).
Run `pipx install pandoc-include` if you want to install the filter.

The tables also have line numbers in LaTeX margin notes. Add the following
somewhere in your LaTeX setup (e.g. in a file included with `pandoc -H`):

```latex
% Margin notes
\usepackage{marginnote}
\renewcommand{\marginpar}{\marginnote}
\reversemarginpar % Moves margin notes to the left margin
\usepackage{ragged2e} % Allows right-aligned text
```

## Bygg

The project includes a set of targets for the [Bygg build system](https://github.com/rikardg/bygg).
Here, it is only used as a simple taskrunner with some rudimentary dependency
management.

To install:
```shell
pipx install bygg
```

To run:
```shell
bygg
```
builds the default target. See `Byggfile.toml` for what the default target is
and the other actions that are available.