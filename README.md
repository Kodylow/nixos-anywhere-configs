# nixos-anywhere-examples

Checkout the [flake.nix](flake.nix) for examples tested on different hosters.

# Steps

1. Install nix with determinate systems installer
```
curl --proto '=https' --tlsv1.2 -sSf -L https://install.determinate.systems/nix | sh -s -- install
```

2. Clone this repo
```
git clone https://github.com/kodylow/nixos-anywhere-configs.git
```

3. Make an ephemeral SSH key
```
ssh-keygen -t ed25519 -C "your_email@example.com"
```

4. Stick the public key in the authorized_keys of the configuration.nix
```
cat /root/.ssh/id_ed25519.pub
```

5. Run the flake replacing the ip with your target
```
nix run github:nix-community/nixos-anywhere -- --flake .#digitalocean root@<ip>
```
