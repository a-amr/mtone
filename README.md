What is mtone?

MTONE stands for Multi to One, which enables all keyboards to act as one keyboard in Linux.

This app makes using multiple keyboards with the same machine workflow flawlessly. Without it, for example, you can't press shift on one keyboard and press a key on another keyboard. Also, some cheap split keyboards wouldn't work due to the design of the kernel driver.

## usage

mergeinputs inputeventpaths
simply
```plain
 mergeinputs /dev/input/by-path/*-kbd
```

you might either need the `input` group or run mergeinputs as root.
to add to input 
```sudo usermod -aG  input yourusername 
```

## but how does it work?
by Leveraging the uinput module, Mergeinputs is able to sit before any userspace input drivers:

/dev/input/eventx /dev/input/eventy -> Mergeinputs grabs all key events -> "merged input" device -> input drivers -> userspace applications

This means any application will only see one keyboard (merged inputs) pressing keys, eliminating any issues multiple devices might have caused.

## install

`make install`

There is no systemd service for the app. This is an independent Linux app that works on any distro with any init.
