---
title: Restoring SSH Keys
date: '2019-04-6'
spoiler: You need the correct permission
---



Recently I made the foolish decision to upgrade my machine from Ubuntu 18.04 to Ubuntu 19.04. Unfortunately, after performing the upgrade I wasn't able to get the machine to boot :(. After rebuild, I needed to restore SSH keys from backup. When I tried to use a key to log into a remote server I got the message:

```console
sign_and_send_pubkey: signing failed: agent refused operation
userName@###.###.##.###: Permission denied (publickey).
```

The problem is that when I copied the SSH keys from back to ~/.ssh, the permissions were too open so the keys were rejected. The fix is pretty quick.

The ~/.ssh folder should have the permissions `drwx------` If these are not the current permissions change them via:
```console
chmod 700 ~/.ssh
```

The `authorized_keys` file and the SSH keys themselves should have the permissions `-rw-------`. If these are not the current permissions change them via (if the key name is 'some-server'):

```console
chmod 600 ~/.ssh/authorized_keys
chmod 600 ~/.ssh/some-server
chmod 600 ~/.ssh/some-server.pub
```

After this all should be working.



