# ZeroMount Ace 5 hardening — experimental

Target: OnePlus Ace 5 (CPH2691), Snapdragon 8 Gen 3 (SM8650 / pineapple), Android 16 device configuration, Android 14 / Linux 6.1 kernel source.

## Changes
- Make the ZeroMount Kconfig option opt-in by default; the dedicated Ace 5 build explicitly enables it.
- Treat an empty rule set as a disabled state in the kernel's common ZeroMount skip guard.
- Refuse to enable the VFS engine when no rules are registered.
- Disable the VFS engine when the last rule is removed.
- Disable the engine before clearing all rules.
- Prevent static virtual-path lookup from returning mappings while the engine is disabled or has no rules.
- Add a dedicated Ace 5 build workflow that uses `configs/a16/OP-ACE-5.json` and performs a full compile (not snapshot-only).
- Publish a checksummed flashable ZIP only after the build action completes successfully.

## Important safety notes
- This is an experimental compatibility build, not a claim that ZeroMount is fully validated on CPH2691 / Android 16 / kernel 6.1.141.
- The earlier black-screen event has not been conclusively root-caused. These changes harden empty-rule activation but do not replace a complete kernel-source audit or real-device validation.
- Do not install this on a daily-use phone until recovery/rollback is prepared and the build logs and package contents have been reviewed.
- No device flashing or on-device testing is performed by this workflow.
