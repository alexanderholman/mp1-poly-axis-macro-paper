# Installation

## Prerequisites

- Git
- Python 3.11+
- Optional: LaTeX distribution for manuscript builds

## Clone

```bash
git clone git@github.com:alexanderholman/mp1-poly-axis-macro-paper.git
cd mp1-poly-axis-macro-paper
```

## Update

```bash
git pull --ff-only
```

## MP1 tools

Install the pinned `mp1-tools` version recorded in `mp1_tools.lock`:

```bash
python -m pip install "git+ssh://git@github.com/alexanderholman/mp1-tools.git@460e5ca3e4882db5c38466c34f887a4887b06dbf"
```

For local development, a submodule checkout is available at `vendor/mp1-tools`.

## Remove

Delete the cloned directory when no longer needed.
