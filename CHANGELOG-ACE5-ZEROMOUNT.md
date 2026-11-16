# ZeroMount hardening — OP13R kernel for OnePlus Ace 5 (experimental)

## Intended setup

- **Physical device:** OnePlus Ace 5 (CPH2691), Snapdragon 8 Gen 3 / SM8650 (pineapple)
- **ROM base:** OnePlus 13R-derived ROM
- **ODM:** Ace 5 ODM, as used in the user's existing ROM setup
- **Kernel source:** OnePlus 13R Android 16 configuration, Android 14 / Linux 6.1.141
- **Build config:** `configs/a16/OP13r-6.1.141.json`
- **Source manifest:** `manifests/a16/oneplus_13r_6.1.141_w.xml`

This is deliberately an **OP13R-source kernel for the user's 13R-based ROM + Ace 5 ODM setup**. It is not a native Ace 5-source kernel build.

## ZeroMount changes
- Make the ZeroMount Kconfig option opt-in by default; the dedicated build explicitly enables it.
- Treat an empty rule set as a disabled state in the kernel's common ZeroMount skip guard.
- Refuse to enable the VFS engine when no rules are registered.
- Disable the VFS engine when the last rule is removed.
- Disable the engine before clearing all rules.
- Prevent static virtual-path lookup from returning mappings while the engine is disabled or has no rules.
- Adapt the ZeroMount integration hunks to the SUSFS-patched Linux 6.1 source layout, including the readdir injection paths.
- Build the full kernel, verify the flashable ZIP, generate SHA-256 checksums, and publish an experimental release only after all prior steps succeed.

## Important safety notes
- This is an experimental compatibility build. CI success proves that the selected OP13R 6.1.141 source compiles and packages; it does not prove the resulting kernel is safe on every CPH2691 ROM/ODM combination.
- The earlier black-screen event has not been conclusively root-caused. Empty-rule hardening does not replace a full kernel-source audit or real-device validation.
- Before flashing, confirm that the installed 13R-derived ROM is using the matching 6.1.141 kernel/vendor-module interface and that the Ace 5 ODM setup is still in place.
- Prepare a known-good boot image and recovery/rollback path first.
- No device flashing or on-device testing is performed by this workflow.
