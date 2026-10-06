# dlorg_elliot_hornstein

Lab för DLORG

# DLORG - Download Organizer
Watches your `~/Downloads` folder and automatically moves new files into the right subfolder based on their extension.

# What it does

When a file is created, finished writing, or moved into `~/Downloads`, the script:

1. Looks at the file extension
2. Creates the target folder if it doesn't exist
3. Moves the file there

# Requirements
```bash
# inotify-tools
sudo dnf install inotify-tools
```

# How to run
Download the script from github
```bash
# Make sure the script is executable
chmod +x dlorg

# Run it
./dlorg
```

You will see:
```
watching /home/you/Downloads
```
# Now open a tmux session

1. Start tmux and split the window (`Ctrl-b` then `%`)
2. In one pane run `./dlorg.`
3. In the other pane go to Downloads and create test files:

```bash
cd ~/Downloads
touch notes.docx beautiful.jpg coolu.png awesome_{1..3}.mp4 cool_{1..3}.pdf a.txt b.txt
```

You should see the files being moved and messages like:

```
notes.docx -> docs/
beautiful.jpg -> images/
awesome_1.mp4 -> videos/
```
You can also `mv` files into Downloads from somewhere else.
```bash
mv text.txt ~/Downloads/
# it should move back
```
The `images/` folder is recreated automatically and the file is moved.     
```bash
rm -r ~/Downloads/images
touch ~/Downloads/image.png
```

Move file from host to linux. From a Windows terminal (Powershell or CMD)
```bash
scp "C:\Users\Administrator\Downloads\asd.gif" user@hostname:~/Downloads/
```

