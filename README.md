# swift-worktree-sim

Give every Git worktree its own iOS Simulator and DerivedData directory.

Parallel builds of the same iOS app normally share one simulator install slot per bundle identifier. One agent or developer can silently replace another worktree's build, leaving screenshots and manual verification pointed at the wrong source. `worktree-sim` keys both the simulator device and DerivedData to the worktree's absolute path.

## Requirements

- macOS with Xcode and an installed iOS Simulator runtime
- Bash 3.2 or newer
- Python 3 as shipped with Xcode/macOS

## Install

Copy `bin/worktree-sim` into your repository or onto your `PATH`, then make it executable.

```sh
chmod +x bin/worktree-sim
bin/worktree-sim run
```

The tool automatically discovers a single root-level `.xcodeproj` or `.xcworkspace` and derives the scheme from its name. Override discovery when needed:

```sh
WORKTREE_SIM_PROJECT="$PWD/MyApp.xcodeproj" \
WORKTREE_SIM_SCHEME="MyApp" \
WORKTREE_SIM_APP_NAME="MyApp" \
bin/worktree-sim run
```

## Commands

`udid`, `name`, `dd`, `modulecache`, `boot`, `build`, `run`, `shot`, `logs`, `open`, `last`, `status`, and `release`.

Run `release` when a worktree is removed so its simulator is deleted. Build products remain inside that worktree's ignored `build/` directory.

## Configuration

- `WORKTREE_SIM_ROOT`
- `WORKTREE_SIM_PROJECT` or `WORKTREE_SIM_WORKSPACE`
- `WORKTREE_SIM_SCHEME`
- `WORKTREE_SIM_APP_NAME`
- `WORKTREE_SIM_DEVICE` (default `iPhone 17`)
- `WORKTREE_SIM_CONFIG` (default `Debug`)
- `WORKTREE_SIM_DEVICE_PREFIX` (default `Worktree`)
- `WORKTREE_SIM_MODULE_CACHE`

No credentials, signing material, application source, or simulator contents are transmitted or persisted outside the local worktree and Apple's Simulator directories.

## License

MIT. See `LICENSE`.
