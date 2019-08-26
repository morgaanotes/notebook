# OSX install notes (2019)

## What to install

- Firefox (Developer Edition) + Sign In + Make Default + Set DDG as search engine and remove others
- Alfred ([https://www.alfredapp.com/](https://www.alfredapp.com/))
- Spectacle ([https://www.spectacleapp.com/](https://www.spectacleapp.com/))
- Clipy ([https://clipy-app.com/](https://clipy-app.com/))
- Dropbox
- Homebrew (/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)")
- KeepassXC (brew cask install keepassxc)
- Notion ([https://keepassxc.org/download/](https://keepassxc.org/download/))
- Todoist (via App Store + in browser)
- Vim (brew install vim)
- Clone your dot files repo and follow instructions
- Ack (brew install ack)
- editorconfig (brew install editorconfig)
- nvm (brew install nvm)
- Configure Finder to your will
- ag (brew install the_silver_searcher)
- fzf (brew install fzf)
- [bat]([https://github.com/sharkdp/bat](https://github.com/sharkdp/bat)), A cat(1) clone with wings. (brew install bat). Used by vim fzf preview to render syntax highlighting

## Configuring your shell

### zsh

#### Install

If on macOS: `brew install zsh zsh-completions`
Otherwise:
Check the [How to install zsh in many platforms](https://github.com/robbyrussell/oh-my-zsh/wiki/Installing-ZSH#how-to-install-zsh-in-many-platforms)

#### Oh my zsh

Install via curl:
  `sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"`
