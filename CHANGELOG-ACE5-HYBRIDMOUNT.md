# Hybrid Mount VFS — OP13R kernel 6.1.157 for OnePlus Ace 5 (experimental)

## Intended setup

- **Physical device:** OnePlus Ace 5 (CPH2691), Snapdragon 8 Gen 3 / SM8650 (pineapple)
- **ROM base:** OnePlus 13R-derived ROM
- **ODM:** Ace 5 ODM
- **Kernel source:** OnePlus 13R Android 14 / Linux 6.1.157, built for the Android 16 configuration
- **Build config:** `configs/a16/OP13r-6.1.157.json`
- **Source manifest:** `manifests/a16/oneplus_13r_6.1.157_w.xml`
- **Common kernel commit:** `7a7ae28e849b0f9b42b8b6fc26feebe1864bf7ac`
- **Modules/device-tree commit:** `dda73f7205501c09f7d0f48fd5f6d7f4b2220ca7`

This is a separate OP13R-source kernel variant for the same 13R-ROM + Ace 5 ODM setup.

## Hybrid Mount integration

- Integrate the Hybrid Mount VFS kernel provider into `fs/hybridmount/`.
- Pin the provider sources to Hybrid Mount `v6.2.6` (`0a047415b795e760bfdb84e98ef7d4b653485c50`).
- Enable `CONFIG_HYBRIDMOUNT=y` so the provider is built into the kernel rather than relying on a separately loaded VFS LKM.
- Keep ZeroMount entirely disabled and do not apply the ZeroMount patch in this variant.
- The matching Hybrid Mount manager/meta-module remains a separate installation: [Hybrid Mount v6.2.6 release](https://github.com/Hybrid-Mount/meta-hybrid_mount/releases/tag/v6.2.6).

## Important safety notes

- This is an experimental compatibility build. A successful CI build verifies compilation and packaging, not real-device behavior on every CPH2691 ROM/ODM combination.
- This is a separate alternative to the ZeroMount build; do not combine the two VFS implementations in one kernel image.
- The kernel's built-in VFS provider is specifically for Hybrid Mount's VFS backend and does not make ZeroMount rules compatible with Hybrid Mount.
- Confirm the installed ROM's kernel/vendor-module interface and Ace 5 ODM setup before flashing.
- Prepare a known-good boot image and recovery/rollback path first.
- No device flashing or on-device testing is performed by this workflow.
