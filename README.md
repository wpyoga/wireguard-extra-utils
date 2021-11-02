## wireguard-extra-utils

A collection of utilities to simplify WireGuard node configuration.

### wg-dir

Allows WireGuard configuration in the form of 'drop-in directory'. Instead of editing the file `/etc/wireguard/my-mesh.conf`, make configuration fragments in `/etc/wireguard/my-mesh/` and add/remove peers by adding and removing peer config fragments. `wg-dir` reads the fragments and creates `/etc/wireguard/my-mesh.conf` that can be used by `wg-quick` or `wg`.

