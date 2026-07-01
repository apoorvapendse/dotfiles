# Dotfiles (private backup)

Personal Arch + **dwm** setup. Suckless sources live in a separate public repo.

## Repos

| Repo | What |
|------|------|
| **[apoorvapendse/suckless](https://github.com/apoorvapendse/suckless)** | dwm / st / dmenu sources, `dwm-session`, `safari-saver`, `install.sh` |
| **this repo** | shell, nvim, xinitrc, helper binaries (incl. Safari Drive binary) |

## Restore (quick)

```sh
# suckless WM stack
git clone https://github.com/apoorvapendse/suckless.git ~/src/suckless
cd ~/src/suckless && ./install.sh

# home files from this repo
git clone https://github.com/apoorvapendse/dotfiles.git ~/src/dotfiles
cd ~/src/dotfiles
cp -a .zshrc .bashrc .xinitrc ~/
mkdir -p ~/.config/nvim ~/.local/bin
cp -a .config/nvim/init.lua ~/.config/nvim/
cp -a bin/* ~/.local/bin/
chmod +x ~/.local/bin/*

# idle screensaver deps
sudo pacman -S --needed xss-lock xorg-xset slock
```

Log in via `~/.xinitrc` or the **dwm (safe restart)** session so `dwm-session` runs.

### Idle lock (Safari Drive → slock)

- **60s** idle → fullscreen Safari Drive (`safari-saver` → `safari-linux`)
- **+60s** idle → `slock`
- **Super+L** → immediate `slock`

Binary: `bin/safari-linux` → `~/.local/bin/safari-linux`.

## Layout

```
.bin/                  # optional copy of ~/.local/bin helpers
bin/dwm-session
bin/safari-saver
bin/safari-linux       # Safari Drive (large binary)
bin/dailynote
.config/nvim/init.lua
.xinitrc               # exec ~/.local/bin/dwm-session
.zshrc / .bashrc
```

