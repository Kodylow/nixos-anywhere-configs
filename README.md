# nixos-anywhere-configs

Run this from another machine, you run this and it reformats the target then you ssh into the target which will now be running nixos.

# Steps

1. Install nix with determinate systems installer
```
curl --proto '=https' --tlsv1.2 -sSf -L https://install.determinate.systems/nix | sh -s -- install
```

2. Clone this repo
```
git clone https://github.com/kodylow/nixos-anywhere-configs.git
```

3. Make an SSH key
```
ssh-keygen -t ed25519 -C "kodylow7@proton.me"
```

4. Stick the public key in the authorized_keys of the configuration.nix
```
sed -i '/users.users.root.openssh.authorizedKeys.keys/,/];/ c\  users.users.root.openssh.authorizedKeys.keys = [\n    "'"$(cat ~/.ssh/id_ed25519.pub)"'"\n  ];' nixos-anywhere-configs/configuration.nix
```

5. Copy the public key to the target machine

```
ssh-copy-id -i id_ed25519.pub root@<ip>
```

5. cd into the dir and Run the flake replacing the ip with your target
```
cd nixos-anywhere-configs
nix run github:nix-community/nixos-anywhere -- --flake .#digitalocean root@<ip>
```
