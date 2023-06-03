# dotfiles Setup Instructions

The followings steps illustrate how to setup my [dotfiles](https://github.com/manuelfuchs/dotfiles). This solution is based on [Nicola Paolucci's post](https://www.atlassian.com/git/tutorials/dotfiles).

```zsh
# Clone dotfiles configuration into ~/.cfg folger
echo ".cfg" >> .gitignore
git clone --bare https://github.com/manuelfuchs/dotfiles.git $HOME/.cfg

# Setup config alias for current shell session
alias config='/usr/bin/git --git-dir=$HOME/.cfg/ --work-tree=$HOME'

# Checkout dotfiles configuration and configure file tracking
config checkout
config config --local status.showUntrackedFiles no

# Install homebrew
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

# Install software defined in Brewbundle file
/opt/homebrew/bin/brew bundle install

# Set fish as default shell
echo /opt/homebrew/bin/fish | sudo tee -a /etc/shells > dev/null
chsh -s /opt/homebrew/bin/fish
```

## Usage

To check in any additional dotfiles, either use the `config` command (alias for `git` command targeting `~/.cfg` folder specifically) or `config-update <asdf / brew / fish>`.
