# ~/.bashrc

[[ $- != *i* ]] && return

# General aliases
alias ls='ls --color=auto'
alias grep='grep --color=auto'
alias ..='cd ..'
alias ...='cd ../..'
alias c='clear'
PS1='[\u@\h \W]\$ '

# Git
alias gs='git status'
alias ga='git add .'
alias gc='git commit -m'
alias gp='git push'
alias gpl='git pull'
alias gco='git checkout'
alias gl='git log --oneline --graph --all'

# Web Development
alias serve='php -S localhost:8000'
alias npmi='npm install'
alias npms='npm start'
alias npmb='npm run build'

# i3 / Display
alias restart-i3='i3-msg restart'
alias reload-i3='i3-msg reload'
alias xrandr-list='xrandr | grep " connected"'
alias killx='sudo systemctl restart display-manager'

# Project initialization
mkproj() { mkdir -p "$1" && cd "$1" && git init && code .; }

# Optional replacements, check if installed
if command -v bat &> /dev/null; then alias cat='bat'; fi
if command -v btop &> /dev/null; then alias top='btop'; fi
if command -v fd &> /dev/null; then alias find='fd'; fi
if command -v rg &> /dev/null; then alias rg='ripgrep'; fi
if command -v neofetch &> /dev/null; then alias sys='neofetch'; fi

# Distro-specific aliases
if [ -f /etc/os-release ]; then
    . /etc/os-release
    case "$ID" in
        arch)
            alias update='sudo pacman -Sy'
            alias upgrade='sudo pacman -Syu'
            alias install='sudo pacman -S'
            alias remove='sudo pacman -Rns'
            alias cleanup='sudo pacman -Rns $(pacman -Qtdq)'
            alias emptycache='sudo pacman -Sc'
            alias emptytrash='rm -rf ~/.local/share/Trash/files/* ~/.local/share/Trash/info/*'
            alias yays='yay -S'
            alias yayr='yay -Rns'
            alias yaysy='yay -Sy'
            alias yaysyu='yay -Syu'
            ;;
        ubuntu|debian)
            alias update='sudo apt update'
            alias upgrade='sudo apt upgrade'
            alias install='sudo apt install'
            alias remove='sudo apt remove'
            alias cleanup='sudo apt autoremove'
            alias emptycache='sudo apt clean'
            alias emptytrash='rm -rf ~/.local/share/Trash/files/* ~/.local/share/Trash/info/*'
            ;;
        fedora)
            alias update='sudo dnf check-update'
            alias upgrade='sudo dnf upgrade'
            alias install='sudo dnf install'
            alias remove='sudo dnf remove'
            alias cleanup='sudo dnf autoremove'
            alias emptycache='sudo dnf clean all'
            alias emptytrash='rm -rf ~/.local/share/Trash/files/* ~/.local/share/Trash/info/*'
            ;;
    esac
fi
