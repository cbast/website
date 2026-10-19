Reproducible (declarative) builds and deployments.

## Create Small Docker Images
- [Building and running Docker images](https://nix.dev/tutorials/nixos/building-and-running-docker-images.html): nix.dev Tutorials

Create nix image definition:
```bash
cat << 'EOF' > hello.nix
{ pkgs ? import <nixpkgs> { }
, pkgsLinux ? import <nixpkgs> { system = "x86_64-linux"; }
}:

pkgs.dockerTools.buildImage {
  name = "hello-docker";
  config = {
    Cmd = [ "${pkgsLinux.hello}/bin/hello" ];
  };
}
EOF
```

Generate Docker image:
```bash
nix-build hello.nix # Outputs image to "result" file
```

Load Docker image:
```bash
docker load < result
```

Run in Docker:
```bash
docker run -t hello-docker:<SHA-1>
```

## References
- [NixOS/nix](https://github.com/NixOS/nix): GitHub Repo
- [NixOS/nix](https://nixos.org/): Official Website
- [Zero to Nix](https://zero-to-nix.com/): An unofficial, opinionated, gentle introduction to Nix.
- [Awsome-nix](https://github.com/nix-community/awesome-nix): A curated list of the best resources in the Nix community.

## Alternatives
- [Ansible](https://www.ansible.com/): Suite of software tools that enables infrastructure as code.
- [OSTree](https://github.com/ostreedev/ostree): Manage multiple bootable versioned filesystem trees.
