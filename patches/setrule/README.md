### Description

This patch adds an ability to add or change client rules at runtime.

The patch only adds one keybinding (`Alt+Shift+R`) to toggle `isfloating`
option, but this can be easily extended if you want to tweak other options as
well. You just need to define a new function similar to `setruleisfloating` and
add a new keybinding to `config.h`.

For example, this is a function I created for my build to toggle `noswallow`
option from the [swallow][swallow] patch:

```c
void
setrulenoswallow(const Arg *arg) {
	Rule *r = getrule(focustop(selmon));
	if (!r)
		return;
	r->noswallow = !r->noswallow;
}
```

[swallow]: /dwl/dwl-patches/src/branch/main/patches/swallow

### Download

- [0.7](/dwl/dwl-patches/raw/branch/main/patches/setrule/setrule.patch)

### Authors

- [Nikita Ivanov](https://codeberg.org/nikitaivanov) ([GitHub](https://github.com/NikitaIvanovV))
