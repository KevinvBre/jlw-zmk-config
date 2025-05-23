# Personal notes:











# jlw's ZMK User Config Repo

## Instructions

### Brand new to ZMK?

1. You will need to [sign up for a GitHub account](https://github.com/signup), and [fork this repository](https://docs.github.com/en/get-started/quickstart/fork-a-repo#forking-a-repository) so you can edit it.
2. Navigate to the **Actions** tab and click the "I understand my workflows, go ahead and run them" button to enable builds.

   ![Actions tab with "I understand my workflows" button](https://i.imgur.com/B7cTAE6.png)
3. Edit the files for your keyboard(s) in the [`config`](config/) folder. `.conf` files configure keyboard features, and `.keymap` files change the keymap. Settings in `default.conf` will apply to all keyboards; to make keyboard-specific changes, create a file named after the keyboard (e.g. `jlwffre.conf`) and change the settings there.
4. Edit the [`build.yaml`](build.yaml) file to include the board(s) and/or shield(s) you need to build firmware for.
5. After committing your changes, your firmware will begin compiling. Assuming there are no typos or other problems, it will eventually be [downloadable from the Actions tab](https://zmk.dev/docs/user-setup#installing-the-firmware).
6. [Flash the firmware](https://zmk.dev/docs/user-setup#flashing-uf2-files) that matches the board and/or shield you're using, e.g. `jlwffre-zmk.uf2`.

### Already have a ZMK user config repo?

The keymaps here may still be useful, but you probably want to [add the `zmk-jlw-keyboards` ZMK module](https://github.com/josh-l-wang/zmk-jlw-keyboards) to your existing `west` manifest instead.

## Common Questions/Problems

### There was an error and the build didn't finish.

#### There is probably an error in your keymap.

[Clicking into the details of the action](https://docs.github.com/en/actions/quickstart#viewing-your-workflow-results) will show the error log. While very long, this log will often show the exact line number causing the problem in your keymap so it is worth reading closely. Check this against the last changes you made.

Keep in mind that each ZMK "keycode" is made up of a [behavior](https://zmk.dev/docs/features/keymaps#behaviors) which always has an `&` in front (e.g. `&kp` for a **k**ey **p**ress), followed by any details for that behavior.
Resetting to bootloader is just [`&bootloader`](https://zmk.dev/docs/behaviors/reset) while the letter `Z` is [`&kp Z`](https://zmk.dev/docs/behaviors/key-press). And "select Bluetooth profile #1" is [`&bt BT_SEL 1`](https://zmk.dev/docs/behaviors/bluetooth)). Read [the docs](https://zmk.dev/docs/) closely.

### After disconnecting the keyboard from Bluetooth, it won't reconnect.

#### Forget the Bluetooth connection on both the keyboard and the host, then try re-pairing.

If you don't remember which profile on the keyboard was used to connect to a specific host, you may have to clear them all. [See ZMK's documentation for more information](https://zmk.dev/docs/behaviors/bluetooth#bluetooth-pairing-and-profiles).

As a last resort, try flashing the `settings_reset` firmware for your board; this will force-clear everything.

## Further Troubleshooting Resources

- [ZMK's troubleshooting page](https://zmk.dev/docs/troubleshooting)
- Stop by the jlw channel in [the 40s Discord](https://discord.gg/40percent)
- Ask the ZMK experts in [ZMK's Discord](https://zmk.dev/community/discord/invite)
