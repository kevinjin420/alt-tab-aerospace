# alt-tab-macos, AeroSpace fork

Fork of [lwouis/alt-tab-macos](https://github.com/lwouis/alt-tab-macos) with [AeroSpace](https://github.com/nikitabobko/AeroSpace) integration
- per-workspace window filtering
- workspace name badges
- space-based sort

## How it works

Directly querying the aerospace CLI on alt-tab pressed leads to significant amounts of lag and freezing. This implementation uses a cache that is kept warm via aerospace event hooks. This means that, for this setup to wokr, your `aerospace.toml` needs to be modified to call the alt-tab CLI server with aerospace event updates, including:
- workspace changes
- window moves

Window destruction events are handled natively by `AltTab`

## AeroSpace config

You need to set up hooks on 

```toml
exec-on-workspace-change = ['/bin/bash', '-c', '/Applications/AltTab.app/Contents/MacOS/AltTab --aerospace-workspace-changed=$AEROSPACE_FOCUSED_WORKSPACE']

[[on-window-detected]]
check-further-callbacks = true
run = ['exec-and-forget /bin/bash -c "/Applications/AltTab.app/Contents/MacOS/AltTab --aerospace-mapping-changed"']

# append to each move-node-to-workspace binding:
# 'exec-and-forget /bin/bash -c "/Applications/AltTab.app/Contents/MacOS/AltTab --aerospace-mapping-changed"'
```

Note that the alt tab executable path is hard coded here, as toml doesn't support variables. Modify your `aerospace.toml` to target where your `AltTab` binary lives. 

My sample aerospace.toml could be found [here](https://github.com/kevinjin420/dotfiles/blob/main/config/aerospace/aerospace.toml)

## Install

Download `AltTab.zip` from [latest release](../../releases/latest), unzip to `/Applications/`, then:

```bash
xattr -dr com.apple.quarantine /Applications/AltTab.app
```