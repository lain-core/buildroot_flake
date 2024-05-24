# buildroot_flake

Simple flake builds buildroot projects on nixos modified to build [GarlicOS](https://github.com/GarlicOS/buildroot) and other Anbernic Custom Firmware packages through buildroot.

Buildroot hardcodes `/usr/bin/` paths, which is why this project uses
a `FHSuserEnv` instead of a basic `mkShell`.

The cross toolchain used is `AARCH64` but can be modified for other
architectures by modifying the `pkgsCross` path to the cross compiling gcc.

## Usage
To use this, enter your target directory and create a basic flake.nix to pull this in:
```nix
{
  inputs = {
    buildroot.url = "github:lain-core/garlicos_buildroot_flake";
  };

  outputs = {
    systems,
    nixpkgs,
    ...
  } @ inputs: {
    devShells = inputs.buildroot.devShells;
  };
}
```

Then, use `nix develop` to enter a shell which pulls in all of the target dependencies. You can then configure using `make menuconfig` as usual and then `make`.
