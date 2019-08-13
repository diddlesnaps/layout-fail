# Snapcraft Layout Fail Test

## Reproducing

Run the following:

```sh
snapcraft
snap install layout-fail_0_amd64.snap --dangerous
layout-fail
snap install layout-fail_0_amd64.snap --dangerous
layout-fail
snap install layout-fail_0_amd64.snap --dangerous
```

The failure is reproducable, and occurs once there are two instances of the snap with an active mount namespace containing the layout. Any attempts to install further instances will fail unless you first run `/usr/lib/snapd/snap-discard-ns layout-fail` or remove the previous instances of the snap with `snap remove`.

You **must** execute a command from the snap to ensure the mount namespace is setup by snapd before installing each iteration. Without running a command from the snap the bug will not be evident.