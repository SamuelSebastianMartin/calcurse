# Calcurse Syncing

for syncing calcurse calendar

## Aim

Rather than syncing the actual `calcurse` directory, I prefer to have my sync files all in one `.sync` directory, and symlink to those files. Therefore, I have a dirctory structure `~/.sync/calcurse`.

## Initial set-up

### 1 Find where your calcurse files are stored.

`find ~ -name calcurse -type d`

or, as one of the files maybe uniquely named, you could use `find ~ -name apts -type f`

On my Manjaro system, the files are in `.local/share/calcurse/`

### 2 Put data in sync directory

Copy the `notes` directory and the `apts` and `todo` files to your `~/.sync/calcurse` directory

```
cd ~/.local/share/calcurse/
cp -r * ~/.sync/calcurse/
```

### 3 Remove or rename existing files.

Rather than delete the contents, you may wish to rename them with `.old`, in case of problems:

```
cd ~/.local/share/calcurse/
ls | xargs -I {} mv {} {}.old
```

### 4 Set up symbolic links to the synced files.

For each item that was is `~/.local/share/calcurse/` make a sym-link

```
ln -s ~/.sync/calcurse/apts apts
ln -s ~/.sync/calcurse/notes notes
ln -s ~/.sync/calcurse/todo todo
```

### 5 Sync setup

Less everyday than the above, to give the same theme, colours and
settings in new installations, one can also sync the config files.

Set up a similar symlink in `~/.config/calcurse/`, at least for the
`conf` file, which gives. `keys` is only necessary with changed
shortcuts, which I don't use. God knows what the `hooks` directory
is for, but it is empty.
### Finally

commit the `~/.sync/calcurse/` changes to github

## Adding a synchronised system

On the new system, `git clone` the repository into `~/.sync/calcurse/`

Repeat the set-up steps 3 & 4, above.
