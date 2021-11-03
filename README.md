## wireguard-extra-utils

A collection of utilities to simplify WireGuard node configuration.

In the examples below, the WireGuard interface is named `my-mesh`, and the configuration is stored in `/etc/wireguard/my-mesh/`. A configuration fragment is just a few lines of configuration, which when concatenated makes a complete `wg-quick` config file format.

### wg-dir

Allows WireGuard configuration in the form of 'drop-in directory'. Instead of editing the file `/etc/wireguard/my-mesh.conf`, make configuration fragments in `/etc/wireguard/my-mesh/` and add/remove peers by adding and removing peer config fragments.

The executable `wg-dir` reads the fragments and creates `/etc/wireguard/my-mesh.conf` that can be used by `wg-quick` or `wg`. If installed from a package, `wg-dir` is usually found in `/usr/bin`.

### wg-quick-auto-restart (systemd units)

Watch `/etc/wireguard/my-mesh` for changes and restarts wg-quick. To add, remove, or modify a peer configuration, just add, remove, or modify a peer configuration fragment, and the interface will be automatically reloaded.

This depends on `wg-dir`. The files `wg-quick-auto-restart@.path` and `wg-quick-auto-restart@.service` should be installed into `/lib/systemd/system`. It can be enabled with this command:

```shell-session
# systemctl enable --now wg-quick-auto-restart@my-mesh.path
```

### wg-quick-dir (systemd service)

Brings up `my-mesh` using the configuration inside `/etc/wireguard/my-mesh`. It does this by running `wg-dir` and then `wg-quick`. The systemd unit file itself is a modified version of `wg-quick@.service` of wireguard-tools.

## TODO

Maybe check for invalid syntax before overwriting the config file.

Get `wg-dir`'s features included in the official wireguard-tools project.

## License

This project is licensed under the GNU GPL v2, in accordance with the [wireguard-tools](https://git.zx2c4.com/wireguard-tools) project.

