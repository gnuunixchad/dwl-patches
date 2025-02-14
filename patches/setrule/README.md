### Description

This patch adds an ability to add or change client rules at runtime.

The patch only adds one keybinding (`Alt+Shift+R`) to toggle `isfloating`
option. Upon pressing it, dwl will try to find a matching rule for the focused
client and change its `isfloating` setting. If there's no such a rule, a new
rule will be added. The new rule will inherit an appid of the focused client.

It's very easy to add support for more rule options from other patches as well.
You just need to define a new function similar to `setruleisfloating` and add a
new keybinding to `config.h`. For example, this is a function I created for my
build to toggle `noswallow` option from the [swallow][swallow] patch:

```c
void
setrulenoswallow(const Arg *arg)
{
	Rule *r = getrule(focustop(selmon));
	if (!r)
		return;
	r->noswallow = !r->noswallow;
}
```

**NOTE**: This patch makes it impossible to have rules with `NULL` title *and*
appid (such a rule is used internally to mark the end of `rules` array).

**NOTE:** If you happen to apply patches that add new options to the rules, make
sure to update `rule_default` variable in `config.h` as well. This variable is
used for newly created rules.

[swallow]: /dwl/dwl-patches/src/branch/main/patches/swallow

### Download

- [0.7](/dwl/dwl-patches/raw/branch/main/patches/setrule/setrule.patch)

### Authors

- [Nikita Ivanov](https://codeberg.org/nikitaivanov) ([GitHub](https://github.com/NikitaIvanovV))
