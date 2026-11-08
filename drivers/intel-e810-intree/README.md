# Intel E800 series patched in-tree driver extension

The kernel's own `ice` driver, with the TX scheduler burst size and VF
rate-limit patches Media Transport Library carries for Intel's out-of-tree
driver, and a handler for `VIRTCHNL_OP_CONFIG_QUEUE_TC_MAP` ported from that
driver. DPDK's iavf sends that message when it commits a per-queue rate
limit, and the unpatched driver refuses it. The kernel's `irdma` is rebuilt
against this `ice`.

The handler has had no upstream review. The in-tree VF interface has no
`VIRTCHNL_VF_LARGE_NUM_QPAIRS`, so a VF has at most 16 queue pairs.

## Installation

See [Installing Extensions](https://github.com/siderolabs/extensions#installing-extensions).

The modules are built in the fork of siderolabs/pkgs, whose kernel build
signs them with a key the released Talos kernel does not hold. A node loads
them only when booted without `module.sig_enforce`.

## Usage

Talos runs depmod over the extension modules with `search extras built-in`,
so `ice` and `irdma` resolve to the modules here and the in-tree ones are
not loaded. They load on device match, with no machine configuration.

Both have to come from this extension: the kernel's `irdma` imports symbols
from `ice`, and this `irdma` is built against the CRCs this `ice` exports.

The DDP package is the one `intel-ice-firmware` installs.
