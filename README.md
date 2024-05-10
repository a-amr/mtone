Ckath/mergeinputs.

This repo is a fork  of Ckath/mergeinputs.



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

there is no systemd service for the app this is an independent linux app that work in any distro with any init 
