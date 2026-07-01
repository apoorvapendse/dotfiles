# Dotfiles

Public Arch Linux + **dwm** configs and small helper scripts.

Suckless **sources** (dwm / st / dmenu + `install.sh`):  
https://github.com/apoorvapendse/suckless

## Not in this repo

| Thing | Why |
|-------|-----|
| `safari-linux` binary | Third-party binary — keep local only (`~/.local/bin/safari-linux`) |
| SSH keys, tokens, `auth.json` | Secrets |
| Browser / OMZ / nvm trees | Huge or installable elsewhere |
| Real `.gitconfig` identity | Copy from `.gitconfig.example` |

## Layout

| Path | Notes |
|------|--------|
| `.zshrc` / `.bashrc` / `.bash_profile` | Shell (Oh My Zsh on zsh) |
| `.xinitrc` | `exec ~/.local/bin/dwm-session` |
| `.tmux.conf` | vi mode, mouse, yank → xclip |
| `.gitconfig.example` | identity + `gh` credential helper |
| `.config/nvim/init.lua` | system clipboard |
| `.config/neofetch/` | neofetch |
| `.config/gtk-3.0/` | GTK prefs |
| `.config/htop/htoprc` | htop |
| `.config/mimeapps.list` | default browser handlers |
| `.config/environment.d/clipboard.conf` | `DISPLAY=:0` for clipboard tools |
| `.config/touchegg/touchegg.conf` | gestures |
| `.config/touchpad/40-libinput.conf` | libinput snippet → often `/etc/X11/xorg.conf.d/` |
| `.config/fish/completions/grok.fish` | Grok CLI fish completion |
| `.grok/config.toml` | Grok Build UI prefs (no secrets) |
| `bin/dwm-session` | safe dwm restart + **xss-lock** idle lock |
| `bin/safari-saver` | EWMH fullscreen wrapper for Safari Drive under dwm |
| `bin/dailynote` | daily note in st + nvim (`DAILYNOTE_DIR` / `~/Documents/Vault`) |
| `bin/clipfssmon` / `cliprssmon` | external monitor screenshot → clipboard |
| `bin/fssmon` / `rssmon` | external monitor screenshots |
| `bin/fix-grok-clipboard` | Grok binary update helper |
| `dockerinstall.txt` | old Docker Desktop notes |

## Install

```sh
git clone https://github.com/apoorvapendse/suckless.git ~/src/suckless
cd ~/src/suckless && ./install.sh

git clone https://github.com/apoorvapendse/dotfiles.git ~/src/dotfiles
cd ~/src/dotfiles
cp -a .zshrc .bashrc .bash_profile .tmux.conf .xinitrc ~/
cp -n .gitconfig.example ~/.gitconfig   # then edit name/email
mkdir -p ~/.config ~/.local/bin ~/.grok
cp -a .config/* ~/.config/
cp -a .grok/config.toml ~/.grok/
cp -a bin/* ~/.local/bin/
chmod +x ~/.local/bin/*

# idle screensaver + lock (optional Safari Drive binary placed by you)
sudo pacman -S --needed xss-lock xorg-xset slock xclip scrot tmux
# install Safari Drive as ~/.local/bin/safari-linux if you use that path
```

Log in via **xinitrc** or **dwm (safe restart)** so `dwm-session` runs.

### Idle lock

- **60s** idle → fullscreen Safari Drive (if `safari-linux` + `safari-saver` present)
- **+60s** → `slock`
- **Super+L** → lock now

Touchpad snippet (as root, if you use it):

```sh
sudo cp ~/.config/touchpad/40-libinput.conf /etc/X11/xorg.conf.d/
```
