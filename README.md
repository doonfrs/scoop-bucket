# All-in-One Messenger Hub - Scoop bucket

This folder is staged inside the app repo for convenience, but it is meant to live in its
**own separate public repo**: `doonfrs/scoop-bucket`.

## One-time setup

1. Create a new **public** GitHub repo named `scoop-bucket` under the `doonfrs` account.
2. Copy the contents of this folder (`bucket/` and `.github/`) into the root of that new repo and push.
3. Make sure the repo's **default branch is NOT protected** - Excavator commits directly to it.
4. (Optional) Add the `scoop-bucket` GitHub topic to get listed in the public Scoop directory.

## How users install

```powershell
scoop bucket add trinavo https://github.com/doonfrs/scoop-bucket
scoop install all-in-one-messenger-hub
```

## How updates work (zero-touch)

The `excavator.yml` workflow runs every 30 minutes. It reads `bucket/all-in-one-messenger-hub.json`,
checks the latest release in `doonfrs/all-in-one-messenger-hub-releases` via `checkver`, and when a new
version exists it rewrites the `version`/`url` and recomputes the hash via `autoupdate`, then commits.
You do nothing per release except publish the GitHub Release (the app pipeline does that automatically).

The first time, after the first real release exists, trigger the workflow once manually
(Actions tab -> Excavator -> Run workflow) so the manifest jumps from the `1.0.0` placeholder to the
current version.
