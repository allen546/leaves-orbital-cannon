Leaves 
===========

[![Leaves CI](https://github.com/LeavesMC/Leaves/actions/workflows/build.yml/badge.svg)](https://github.com/LeavesMC/Leaves/actions/workflows/leaves.yml)
[![Leaves Download](https://img.shields.io/github/downloads/LeavesMC/Leaves/total?color=0&logo=github)](https://github.com/LeavesMC/Leaves/releases/latest)
[![Discord](https://badgen.net/discord/online-members/5hgtU72w33?icon=discord&label=Discord&list=what)](https://discord.gg/5hgtU72w33)
[![QQ](https://img.shields.io/badge/QQ_Unofficial-815857713-blue)](http://qm.qq.com/cgi-bin/qm/qr?_wv=1027&k=nisbmnCFeEJCcYWBQ10th4Fu99XWklH4&authKey=8VlUxSdrFCIwmIpxFQIGR8%2BXvIQ2II%2Bx2JfxuQ8amr9UKgINh%2BdXjudQfc%2FIeTO5&noverify=0&group_code=815857713)

**English** | [中文](README_cn.md)

> [!NOTE]
> This repository is a port of the orbital cannon paper patch to Leaves, and is completely unrelated to Mojang or Microsoft.
> Special thanks to [Kwilver](https://github.com/Kwilver) for creating [KwilsOrbitalPaper](https://github.com/Kwilver/KwilsOrbitalPaper), which allowed orbital cannons to fire on Paper servers.

> Fork of [Paper](https://github.com/PaperMC/Paper) aims at repairing broken vanilla properties.

> You can see what we modify and fix at [here](https://docs.leavesmc.org/en/leaves/reference/configuration)

## Recommended Leaves Configuration

To run the orbital cannon on this Leaves server, the following configuration settings must be adjusted in `leaves.yml`:

### Required Settings (Functional Parity)
These settings must be changed to restore vanilla physics and portal mechanics needed for the cannon to fire.

| Config Path | Value | Default | Rationale / Why it is needed |
| :--- | :--- | :--- | :--- |
| `settings.modify.mc-technical-survival-mode` | `true` | `false` | Restores standard vanilla technical survival mechanics that Paper patches out. |
| `settings.modify.minecraft-old.allow-entity-portal-with-passenger` | `true` | `false` | Allows vehicles with passengers (like items or minecarts) to pass through portals. |
| `settings.modify.minecraft-old.allow-inf-nan-motion-values` | `true` | `false` | Prevents errors and physics issues during extreme velocity launches. |
| `settings.fix.vanilla-portal-handle` | `true` | `false` | Restores vanilla nether portal search and ticking behavior (crucial for stasis chambers). |

### Recommended Settings (Performance Optimization)
These settings prevent the server TPS from dropping to single digits during the stasis charge-up phase.

| Config Path | Value | Default | Rationale / Why it is needed |
| :--- | :--- | :--- | :--- |
| `settings.performance.skip-negligible-planar-movement-multiplication` | `true` | `false` | Skips tiny entity calculations to save CPU cycles when 800+ TNT entities are in stasis. |
| `settings.fix.collision-behavior` | `PAPER` | `VANILLA` | Restores Spottedleaf's optimized collision routines to tick stasis chambers without major lag. |

## How To (Server Admins)
Leaves use the same leavesclip(paperclip fork) jar system that Paper uses.

You can download the latest build (1.21.x) of Leaves by going [here](https://github.com/LeavesMC/Leaves/releases/latest)

You can also [build it yourself](#building).

You can visit our [documentation](https://docs.leavesmc.org/leaves/guides/getting-started) for more information.

## How To (Plugin developers)
Leaves-API:
```kotlin
maven {
    name = "leavesmc-repo"
    url = "https://repo.leavesmc.org/snapshots/"
}

dependencies {
    compileOnly("org.leavesmc.leaves:leaves-api:1.21.10-R0.1-SNAPSHOT")
}
 ```

In order to use Leaves as a dependency you must [build it yourself](#building).
Each time you want to update your dependency, you must re-build Leaves.

Leaves-Server:
```kotlin
dependencies {
    compileOnly("org.leavesmc.leaves:leaves:1.21.10-R0.1-SNAPSHOT")
}
 ```

## Building

You need JDK 21 and good Internet conditions

Clone this repo, run `./gradlew applyAllPatches`, then run `./gradlew createMojmapLeavesclipJar` in your terminal.  

You can find the jars in the `leaves-server/build/libs` directory.

## Pull Requests

See [Contributing](docs/CONTRIBUTING.md)

## Special Thanks To:

[<img src="https://user-images.githubusercontent.com/21148213/121807008-8ffc6700-cc52-11eb-96a7-2f6f260f8fda.png" alt="" width="150">](https://www.jetbrains.com)

[JetBrains](https://www.jetbrains.com/), creators of the IntelliJ IDEA, supports Leaves with one of their [Open Source Licenses](https://www.jetbrains.com/opensource/). Leaves recommend using IntelliJ IDEA as your IDE.
