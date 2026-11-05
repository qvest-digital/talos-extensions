# Intel E800 series out-of-tree driver extension

Intel's out-of-tree [ice](https://github.com/intel/ethernet-linux-ice) driver,
built with the patches Media Transport Library carries for it, Intel's
out-of-tree irdma from the same release, and the DDP package released with
that ice.

## Installation

See [Installing Extensions](https://github.com/siderolabs/extensions#installing-extensions).

The modules are built in the fork of siderolabs/pkgs, whose kernel build
signs them with a key the released Talos kernel does not hold. A node loads
them only when booted without `module.sig_enforce`.

## Usage

Talos runs depmod over the extension modules with `search extras built-in`,
so `ice` and `irdma` resolve to the modules here and the in-tree ones are
not loaded. They load on device match, with no machine configuration.

`modinfo ice` and the driver's probe message report the version
`Kahawai_<version>` for this build.

The DDP package is installed to `/usr/lib/firmware/updates/intel/ice/ddp/`,
which the kernel searches before `/usr/lib/firmware/`. It takes precedence
over the package from `intel-ice-firmware` when both extensions are present.

Both modules carry the names of the in-tree drivers, and both have to come
from this extension: the in-tree `irdma` fails on unresolved symbols against
this `ice`, and Intel's README for its `irdma` requires the `ice` of the same
release.
