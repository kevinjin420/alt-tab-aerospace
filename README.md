# alt-tab-macos — AeroSpace fork

Fork of [lwouis/alt-tab-macos](https://github.com/lwouis/alt-tab-macos) with [AeroSpace](https://github.com/nikitabobko/AeroSpace) integration: per-workspace window filtering, workspace name badges, and space-based sort. Cache is hook-driven — no CLI calls on the keypress path.

**Controls → Show windows from Spaces → Current AeroSpace Desktop** to filter by active workspace.

## AeroSpace config

```toml
exec-on-workspace-change = ['/bin/bash', '-c', '/Applications/AltTab.app/Contents/MacOS/AltTab --aerospace-workspace-changed=$AEROSPACE_FOCUSED_WORKSPACE']

[[on-window-detected]]
check-further-callbacks = true
run = ['exec-and-forget /bin/bash -c "/Applications/AltTab.app/Contents/MacOS/AltTab --aerospace-mapping-changed"']

# append to each move-node-to-workspace binding:
# 'exec-and-forget /bin/bash -c "/Applications/AltTab.app/Contents/MacOS/AltTab --aerospace-mapping-changed"'
```

## Install

Download `AltTab.zip` from [latest release](../../releases/latest), unzip to `/Applications/`, then:

```bash
xattr -dr com.apple.quarantine /Applications/AltTab.app
```

---

<div align="center">

<a href="https://alt-tab.app/"><img src="docs/readme/main.svg" alt="AltTab Pro — 7.4M downloads — 15K GitHub stars — Get AltTab"/></a>

<a href="https://jb.gg/OpenSource"><img src="docs/readme/sponsor.svg" alt="Sponsored by JetBrains" width="900"/></a>

</div>
