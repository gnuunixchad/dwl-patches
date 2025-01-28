### Description
Enables hot-reloading of dwl; meaning almost all logic can be changed at runtime.
This obviously requires some black magic so for now there's a glibc 2.0 or later
dependency to this.
In particular this allows for every option in config.h to be changed at runtime.

#### Reloading
To reload rebuild dwl.so, perhaps reinstall it and then run trigger reload function (bound to Mod+Shift+R by default).
This currently calls `notify-send` in order to inform you of a reloading taking place.
So in short:
1. make changes to `config.h` or `dwl.c`
2. run `make` to rebuild dwl.so
3. run `sudo make install` to reinstall dwl


#### Limitations
Reloading the compositor will replace all functionality except for `main`, `setup`, `run` and the reload logic.
Note that you're responsible yourself for reloading ressources like fonts, which may only get acquired once.
A lot of components of dwl will also only get run on a trigger (the tiling for example).
So not every change will be immediate.

#### Note
This patches triggers `-Wpedantic` a bunch (there's no way around this, `dlsym` yields `void*` pointers to functions).
This will show a lot of warnings but cause no errors.
So you may want to disable this compile option in order to get readable compiler output.

#### How?
Most of all dwl functionality is moved into a shared object file `dwl.so`, which can be reloaded at runtime.

### Download
- [0.7](/dwl/dwl-patches/raw/branch/main/patches/hot-reload/hot-reload-0.7.patch)
- [main 2025-02-14](/dwl/dwl-patches/raw/branch/main/patches/hot-reload/hot-reload.patch)
- find the repo for the patch [here](/Sivecano/dwl/src/branch/hot-reload)
### Authors
- [Sivecano](https://codeberg.org/Sivecano)
- Sérécano at [dwl Discord](https://discord.gg/jJxZnrGPWN)
