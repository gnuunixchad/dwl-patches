### Description

This patch adds the ability to pass keys that are specified in the config header globally, similar to Hyprland's approach.
This might deal with Wayland's lack of global shortcuts.

Example:
```
static const PassKeypressRule pass_rules[] = {
	ADDPASSRULE("com.obsproject.Studio", MODKEY, XKB_KEY_Home),
	ADDPASSRULE("discord", 0, XKB_KEY_n),
    /* xkb key is case-insensitive */
};
```

This will pass the `MODKEY + Home` keys to OBS regardless of what client is currently focused, if any.
The string "com.obsproject.Studio" should match the exact appid of the client.

To get the appid use [dwlmsg](https://codeberg.org/notchoc/dwlmsg) or run stock dwl from a terminal then launch the needed application inside, dwl will print all the info to the stdout.

Note that if a popup (like [fuzzel](https://codeberg.org/dnkl/fuzzel)) is focused, no keys will be globally passed.
This is done so these menus don't get closed after hitting some of the global keys.

### Download
- [git branch](https://codeberg.org/korei999/dwl/src/branch/globalkey)
- [2024-06-08](https://codeberg.org/dwl/dwl-patches/src/branch/main/patches/globalkey/globalkey.patch)
### Authors
- [korei999](https://codeberg.org/korei999)
