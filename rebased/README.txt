Rebased SUSFS kernel patch for android13-5.15.220_r00 (Android 13 GKI, fuxi / Xiaomi 13).
Source: susfs4ksu bca0d2333c1a7d717e7278b019d7af7ba1d16005
Notable drift fixes vs upstream:
  - fs/namespace.c: .220 keeps #include <trace/hooks/blk.h> after "internal.h";
    the rebased patch no longer deletes it (upstream workaround removed).
  - fs/proc/task_mmu.c: .220 has #include <trace/hooks/mm.h> between pkeys.h and
    the asm includes, so the susfs_def.h include is inserted right after pkeys.h.
  - fs/susfs.c, include/linux/susfs.h, include/linux/susfs_def.h are created by
    this patch (self-contained; no separate copy step).
Validated: applies to a pristine android13-5.15.220_r00 tree with patch -p1 --fuzz=0, zero rejects.
