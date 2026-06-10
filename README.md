# dotfiles

My personal dotfiles — macOS, zsh + oh-my-zsh, mise for dev tools.

## Prerequisites

- macOS
- [Homebrew](https://brew.sh)
- [oh-my-zsh](https://ohmyz.sh)
- [mise](https://mise.jdx.dev) — `brew install mise`

---

## 1. oh-my-zsh plugins and theme

The zshrc uses four plugins. Two (`git`, `kube-ps1`) are bundled with oh-my-zsh.
The other two must be installed manually into `$ZSH_CUSTOM`.

### zsh-aws-vault

```shell
git clone https://github.com/jonscheiding/zsh-aws-vault \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-aws-vault
```

### agnoster-aws-vault theme

The zshrc sets `ZSH_THEME="agnoster-aws-vault"`, a custom variant of agnoster that
shows the active aws-vault profile. Install it into the custom themes directory:

```shell
# Download or copy the theme file — adjust the source path as needed
cp path/to/agnoster-aws-vault.zsh-theme \
  ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/themes/agnoster-aws-vault.zsh-theme
```

---

## 2. mise — dev tool versions

`mise` manages tools such as: Java, Go, Maven, Gradle, Python, Node, Terraform, kubectl, MySQL, and coreutils.

> **Notes:**
> - `postgres` and `mysql` install full server packages (not client-only). The CLI tools `psql` and `mysql` are included.
> - `coreutils` is the [uutils Rust reimplementation](https://github.com/uutils/coreutils), not GNU coreutils. Behavior is nearly identical.

### Link the global config

```shell
mkdir -p ~/.config/mise
ln -sf "$(pwd)/mise/config.toml" ~/.config/mise/config.toml
```

### Install all tools

```shell
mise install
```

---

## 3. Homebrew system tools

These are not managed by mise — install them via brew:

```shell
brew install \
  gnu-sed \
  gnu-getopt
```

---

## 4. Python / Anaconda

Anaconda is kept for data science environments. It is placed in `PATH` before mise
so that `mise` Python wins by default, but `conda activate <env>` overrides it
for specific environments. Install Anaconda separately from [anaconda.com](https://www.anaconda.com).

---

## 5. Link the zshrc

```shell
ln -f -P ./zsh/zshrc $HOME/.zshrc
```

# Additional iTerm settings:
https://medium.com/@ThisIsUpen/how-to-jump-between-words-in-iterm2-3c22eb5a25ef
https://stackoverflow.com/questions/32757635/how-to-preserve-iterm-folder-location-between-sessions
