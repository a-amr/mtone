

this app make using multiple keyboard with same machine work flowlessly 
without it you can't for example press shift in keybaord and press key on other keyboard 
also some cheap split keybaords wouldn't work duo to the design of the kernel driver

## usage

mergeinputs inputeventpaths
simply
```plain
 mergeinputs /dev/input/by-path/*-kbd
```

depending on your distro you might either need the `input` group or run mergeinputs as root.

## but how does it work?

leveraging the uinput module, mergeinputs is able to sit before any userspace input drivers:

`/dev/input/eventx /dev/input/eventy -> mergeinputs grabs all key events -> "merged input" device -> input drivers -> userspace applications`

this means any application will only see one keyboard (`merged inputs`) pressing keys, eliminating any issues multiple devices might've caused.

## install

`make install`

there is no systemd service for the app this is an independent linux app that work in any distro with any init 
