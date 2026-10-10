# 1.2. Relationship with Debian

The Kali Linux distribution is based on Debian Testing $ ^{9} $ . Therefore, most of the packages available in Kali Linux come straight from this Debian repository.

While Kali Linux relies heavily on Debian, it is also entirely independent in the sense that we have our own infrastructure and retain the freedom to make any changes we want.

# 1.2.1. The Flow of Packages

On the Debian side, the contributors are working every day on updating packages and uploading them to the Debian Unstable distribution. From there, packages migrate to the Debian Testing distribution once the most troublesome bugs have been taken out. The migration process also ensures that no dependencies are broken in Debian Testing. The goal is that Testing is always in a usable (or even releasable!) state.

Debian Testing's goals align quite well with those of Kali Linux so we picked it as the base. To add the Kali-specific packages in the distribution, we follow a two-step process.

First, we take Debian Testing and force-inject our own Kali packages (located in our kali-dev-only repository) to build the kali-dev package repository. This repository will break from time to time: for in-stance, our Kali-specific packages might not be installable until they have been recompiled against newer libraries. In other situations, packages that we have forked might also have to be updated, either to become installable again, or to fix the instability of another package that depends on a newer version of the forked package. In any case, kali-dev is not for end-users.

kali-rolling is the distribution that Kali Linux users are expected to track and is built out of kali-dev in the same way that Debian Testing is built out of Debian Unstable. Packages migrate only when all dependencies can be satisfied in the target distribution.

# 1.2.2. Managing the Difference with Debian

As a design decision, we try to minimize the number of forked packages as much as possible. How- ever, in order to implement some of Kali's unique features, some changes must be made. To limit the impact of these changes, we strive to send them upstream, either by integrating the feature di-rectly, or by adding the required hooks so that it is straightforward to enable the desired features without further modifying the upstream packages themselves.

The Kali Package Tracker $ ^{10} $ helps us to keep track of our divergence with Debian. At any time, we can look up which package has been forked and whether it is in sync with Debian, or if an update

```
^9 https://www.debian.org/releases/testing/
^10 http://pkg.kali.org/derivative/kali-dev/
```