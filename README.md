# Dotfiles (private backup)

Arch Linux + **dwm** home configs and personal scripts.  
Suckless **sources** (dwm/st/dmenu) live in: https://github.com/apoorvapendse/suckless

## Intentionally excluded

SSH private keys, `gh` tokens, Grok `auth.json` / sessions, browser profiles,
Oh My Zsh / nvm install trees, shell history, caches.

## Layout

| Path | Notes |
|------|--------|
| `.zshrc` / `.bashrc` / `.bash_profile` | Shell (OMZ on zsh) |
| `.xinitrc` | `exec ~/.local/bin/dwm-session` |
| `.tmux.conf` | vi mode, mouse, yank → xclip |
| `.gitconfig` | user + `gh` credential helper |
| `.config/nvim/init.lua` | system clipboard |
| `.config/neofetch/` | neofetch |
| `.config/gtk-3.0/` | GTK prefs |
| `.config/htop/htoprc` | htop |
| `.config/mimeapps.list` | Chrome as default browser |
| `.config/environment.d/clipboard.conf` | `DISPLAY=:0` for clipboard tools |
| `.config/touchegg/touchegg.conf` | gestures |
| `.config/touchpad/40-libinput.conf` | libinput (install under `/etc/X11/xorg.conf.d/` if needed) |
| `.config/fish/completions/grok.fish` | Grok CLI fish completion |
| `.grok/config.toml` | Grok Build prefs (paths may need tweak on new machine) |
| `bin/dwm-session` | safe dwm restart loop + **xss-lock** idle |
| `bin/safari-saver` | fullscreen Safari Drive under dwm |
| `bin/safari-linux` | Safari Drive binary (~4.5MB) |
| `bin/dailynote` | vault daily note in st+nvim |
| `bin/clipfssmon` / `cliprssmon` | external monitor screenshot → clipboard |
| `bin/fssmon` / `rssmon` | external monitor screenshots |
| `bin/fix-grok-clipboard` | Grok binary update helper |

## Restore

```sh
# WM sources + install
git clone https://github.com/apoorvapendse/suckless.git ~/src/suckless
cd ~/src/suckless && ./install.sh

# this repo
git clone https://github.com/apoorvapendse/dotfiles.git ~/src/dotfiles
cd ~/src/dotfiles
cp -a .zshrc .bashrc .bash_profile .tmux.conf .xinitrc .gitconfig ~/
mkdir -p ~/.config ~/.local/bin ~/.grok
cp -a .config/* ~/.config/
cp -a .grok/config.toml ~/.grok/
cp -a bin/* ~/.local/bin/
chmod +x ~/.local/bin/*

# idle screensaver + lock
sudo pacman -S --needed xss-lock xorg-xset slock xclip scrot tmux
```

Log in via **xinitrc** or **dwm (safe restart)** so `dwm-session` runs.

### Idle lock

- **60s** idle → fullscreen Safari Drive  
- **+60s** → `slock`  
- **Super+L** → lock now  

Touchpad conf is a *snippet*; on Arch you often install it as root:

```sh
sudo cp ~/.config/touchpad/40-libinput.conf /etc/X11/xorg.conf.d/
```
