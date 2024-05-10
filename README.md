# mergeinputs

# Fork of https://github.com/Ckath/mergeinputs.

This repo is a fork to resolve the problem I was having with kmonad.

I bought a new mechanical keyboard and wanted to make some scripts and layers for it, but I found out that many keyboards and mice split the usb device into 2 or 3 different input devices under /dev/input

This fork will allow you to combine multiple keyboards into one and specify a path for the input event rather than using a randomly generated name under /dev/input/eventX where X is some number.

This allows you to be able to combine the two input devices and access it via the symlinked input event path in kmonad. This is useful so the path will stay static as to not cause problems with the kmonad config file.

Multiple mergeinputs can be ran at once either by spawning a script or modifying the service to conform to your needs.

Some of the information below is irrelevant. I might update it in the future to match the patches I made.

---

## usage

```plain
mergeinputs inputeventpaths
example to merge all keyboards: mergeinputs /dev/input/by-path/*-kbd
```

depending on your distro you might either need the `input` group or run mergeinputs as root.

## but how does it work?

leveraging the uinput module, mergeinputs is able to sit before any userspace input drivers:

`/dev/input/eventx /dev/input/eventy -> mergeinputs grabs all key events -> "merged input" device -> input drivers -> userspace applications`

this means any application will only see one keyboard (`merged inputs`) pressing keys, eliminating any issues multiple devices might've caused.

## install

`make install`

## auto-start and reload on device change

To start the utility on every boot, a sample systemd unit is provided:

```plain
sudo cp mergeinputs.service /etc/systemd/system
sudo systemctl enable --now mergeinputs
```

If you want to restart mergeinputs on device changes to handle hotplugging of keyboards, use the mergeinputs-restart units:

```plain
sudo cp mergeinputs-restart.* /etc/systemd/system
sudo systemctl enable --now mergeinputs-restart.path
```
