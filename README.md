# dlorg – Download Organizer

Watches your `~/Downloads` folder and automatically sorts new files into
subfolders by file type.

## How it works

dlorg uses `inotifywait` to watch `~/Downloads`. When a file is finished
writing, is moved in, or is renamed there, it:

1. Looks at the file extension
2. Creates the target folder if it doesn't exist
3. Moves the file there

## Requirements

```bash
sudo dnf install inotify-tools
```

## Quick start

```bash
git clone https://github.com/elliotdba26/dlorg_elliot_hornstein.git
cd dlorg_elliot_hornstein
chmod +x dlorg
./dlorg
```

![dlorg running](screenshots/running.png)

## Tmux

In a second terminal (or a tmux split, `Ctrl-b` then `%`):

```bash
cd ~/Downloads
touch notes.docx beautiful.jpg coolu.png awesome_{1..3}.mp4 cool_{1..3}.pdf a.txt b.zip 123.mp3 321.pdf torrent.torrent
```

![dlorg moving files](screenshots/tmux-demo.png)

![sorted Downloads folder](screenshots/sorted.png)

Moving files in works too, and deleted folders are recreated:

```bash
mv ~/Desktop/text.txt ~/Downloads/       # ends up in text/
rm -r ~/Downloads/images
touch ~/Downloads/image.png              # images/ is recreated
```

## Run in the background (systemd)

```bash
mkdir -p ~/.local/bin ~/.config/systemd/user
ln -s "path_to/dlorg" ~/.local/bin/dlorg
cp dlorg.service ~/.config/systemd/user/

systemctl --user daemon-reload
systemctl --user enable --now dlorg.service
```

Check status and watch it work live:

```bash
systemctl --user status dlorg.service
journalctl --user -u dlorg.service -f
```

![service status](screenshots/service-status.png)

Stop it with `systemctl --user disable --now dlorg.service`.
