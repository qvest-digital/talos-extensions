# mxlfs extension

Kernel module of [mxlfs](https://github.com/danielclasen/mxlfs), a memory
filesystem for MXL domains.

## Installation

See [Installing Extensions](https://github.com/siderolabs/extensions#installing-extensions).

The module is built in the fork of siderolabs/pkgs, whose kernel build signs
it with a key the released Talos kernel does not hold. A node loads it only
when booted without `module.sig_enforce`.

## Usage

Load the module through the machine config:

```yaml
machine:
  kernel:
    modules:
      - name: mxlfs
```

and mount it where the MXL domain lives, for example `/run/mxl/domain`.
