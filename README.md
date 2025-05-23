# :snowflake: encore-flake

A flake for simplifying installation of the released encore binaries on nix systems.

Try it out by simply running

```shell
$ nix run github:encoredev/encore-flake
```

## Usage

Add as an input in your nix configuration flake

```nix
{
  inputs = {
    # other inputs...
    encore = {
      url = "github:encoredev/encore-flake";
      # optional
      inputs.nixpkgs.follows = "nixpkgs";
    };
  };
}
```

### Only the CLI

Import `encore.packages.default` into your nixos configuration

```nix
# Home manager
home.packages = [
  inputs.encore.packages.${pkgs.system}.encore
];

# NixOS configuration
environment.systemPackages = [
  inputs.encore.packages.${pkgs.system}.encore
];
```

### With Home manager

Import `encore.homeModules.default` into your home manager config

```nix
imports = [
  inputs.encore.homeModules.default
];
```

and use the `programs.encore` options

```nix
{
  programs.encore = {
    enable = true;
    settings = {
      browser = "never";
    };
  };
}
```

You can then keep it up to date by running

```shell
$ nix flake update encore
```
