<!--
# SPDX-FileCopyrightText: Copyright 2025 Eden Emulator Project
# SPDX-License-Identifier: GPL-3.0-or-later

# SPDX-License-Identifier: GPL-2.0-or-later
-->

# Lichii (tasarren fork)

[![Ko-fi](https://img.shields.io/badge/Ko--fi-Support-FF5E5B?logo=ko-fi&logoColor=white)](https://ko-fi.com/tasarren)

A fork of [zortos293/Lichii](https://github.com/zortos293/Lichii), a Nintendo Switch and Switch 2
emulator. This fork works on speed, memory use and stutter, tested mostly with The Legend of Zelda:
Ocarina of Time. It follows Lichii's `nx2` branch; our changes are on the `next` branch.

Downloads: [releases](https://github.com/tasarren/Lichii/releases). Games, keys and firmware are not
included; use only what you legally own.

## Settings for the best speed (Ocarina of Time)

### Pick your PC

Start with the column closest to your setup:

- **Low-end:** A 4 GB graphics card (such as a GTX 1650) and 16 GB RAM, or a Steam Deck.
- **Mid-range:** A 6–8 GB graphics card and 16–32 GB RAM.
- **High-end:** A graphics card with 12 GB or more and at least 32 GB RAM.

| Setting | Low-end | Mid-range | High-end |
|---|---|---|---|
| Shader Pipeline Memory | Low | Low with 16 GB RAM, otherwise Auto | Auto |
| Texture Memory Target | 2 GB | Auto | Auto |
| Ocarina of Time render scale | Performance (1080p) | Balanced (2276×1280) | Native (1440p) |
| Ocarina of Time local shadow size | Quarter | Full, or Half to save memory | Full |
| Upscaler | Native | Native, or try AMD FSR | NVIDIA DLSS on GeForce RTX, otherwise Native or AMD FSR |

A 4 GB card can still run short on video memory with these settings. The Steam Deck shares memory
between the game and graphics. Try the low-end settings there as a starting point, not a promise
of smooth play.

### Where to change the settings

Stop the game. Right-click Ocarina of Time in the game list and choose **Configure Game**. This
opens **Properties**. Changes there apply only to that game.

![Configure Game in the game's right-click menu](docs/images/readme/properties.png)

Use **Emulation > Configure...** to change the defaults. The screenshots show where to find the
controls. Match numbered arrows to the lists below. For settings that depend on your PC, use the
table above rather than the values in the screenshots.

![Configure... in the Emulation menu](docs/images/readme/configure.png)

#### Graphics

1. Set **Resolution** to **1X**.
2. Start with **Frame rate limit (Switch 2)** at **60 Hz**.
3. Set **Upscaler** from the table. **Native** uses the game's own upscaler, which enlarges the
   picture. In Ocarina of Time, **AMD FSR** and **NVIDIA DLSS** work only at **Resolution: 1X**.
   DLSS quality can override the game's render scale.

![Graphics: 1 Resolution, 2 Frame rate limit (Switch 2), 3 Upscaler](docs/images/readme/graphics.png)

#### System

- Set **Shader Pipeline Memory** from the table. **Low** saves RAM by keeping less graphics work
  ready. Familiar areas may pause briefly or show objects late while Lichii rebuilds that work.

  ![Shader Pipeline Memory in System](docs/images/readme/system-memory.png)

- In **Properties**, set **Console Mode** to **Docked** if you want to change the game's render
  scale.

  ![Console Mode in Properties > System with Docked selected](docs/images/readme/console-mode.png)

#### Add-Ons

1. Enable **Max Resolution (built-in)** to change the game's render scale in Docked mode.
2. Enable **FPS Unlock (built-in)** if you set the frame rate limit above **60 Hz** so the game does
   not run too fast.

![Ocarina of Time Add-Ons: 1 Max Resolution (built-in), 2 FPS Unlock (built-in)](docs/images/readme/oot-addons.png)

#### Game

Restart the game after changing either setting.

1. Set **Ocarina of Time render scale** from the table. If your graphics card struggles, try
   **Ultra Performance (720p)**. A lower scale draws fewer pixels, but the picture is softer.
2. Set **Ocarina of Time local shadow size** from the table. **Half** and **Quarter** save video
   memory by drawing shadows for nearby objects at lower detail.

![Ocarina of Time Game tab: 1 render scale, 2 local shadow size](docs/images/readme/oot-game.png)

#### Ext. Graphics (Graphics > Extras in the main settings)

Turn on **Enable asynchronous shader compilation** so Lichii can prepare some graphics work while
you play.

![Enable asynchronous shader compilation in Graphics Extras](docs/images/readme/async-shaders.png)

#### Adv. Graphics (Graphics > Advanced in the main settings)

1. Set **GPU Mode** to **Fast**. **Accurate** is slower and is not needed for Ocarina of Time.
2. Set **Texture Memory Target** from the table. It covers only textures kept for reuse, not all
   video memory. If a low target causes more pauses and your card has room, try **Auto**.
3. If you're running short on video memory, set **ASTC Recompression Method** to **BC3**. It saves
   memory at a small cost to texture detail.
4. Leave **Skip mesh draws that are still building** on (the default). Some pauses are shorter, but
   objects may appear a moment late. Turn it off if you'd rather wait for those objects.
5. Leave **Precache shaders before game start** off. It misses the shaders that cause the longest
   waits in Ocarina of Time.

![Graphics Advanced: 1 GPU Mode, 2 Texture Memory Target, 3 ASTC Recompression Method, 4 Skip mesh draws that are still building, 5 Precache shaders before game start](docs/images/readme/advanced.png)

Keep **Build all cached shaders before game start** on. It can shorten pauses in familiar areas at
the cost of a longer load.

![Build all cached shaders before game start in Graphics Advanced](docs/images/readme/build-cached-shaders.png)

### What to expect when you play

The first time you visit an area, the game can pause for a second or two while Lichii prepares
shaders (the instructions that draw objects and effects). It usually plays more smoothly on later
visits.

In tests with a 60-frame-per-second limit, both Build 3 and Build 4 held that rate in the Market
and at Lake Hylia once shaders were ready. In one first-visit comparison across 15 areas, the
longest pause dropped from 1.9 to 1.6 seconds, but Build 4 spent more time paused overall.

In a separate Build 4 test in the Market at **1X**, Lichii used roughly **9.5 GB of RAM and 5 GB of
video memory** with Auto memory settings and Native render scale. With **Low**, a **2 GB** texture
target and **Performance** render scale together, it used about **8.5 GB of RAM and 4.2 GB of video
memory**. You may see different numbers in other areas or on your PC.

### Set up NVIDIA DLSS on Linux

On Linux, DLSS needs a GeForce RTX card, a compatible NVIDIA driver and the separate
[Lichii DLSS module](https://github.com/tasarren/lichii-dlss/releases).

1. Open **Graphics** and choose **NVIDIA DLSS** under **Upscaler**.
2. If DLSS is not set up, choose one of these options:

   - **Download (1):** Review and accept NVIDIA's license to download the module and DLSS files.
   - **Install from file... (2):** If you already have the files, select `lichii-dlss-module.so`.
     Keep NVIDIA's DLSS model file in the same folder.

   ![Linux DLSS panel before setup: 1 Download, 2 Install from file](docs/images/readme/dlss-download.png)

3. When the panel says **Ready** (1), click **OK** and start the game.

   ![Linux DLSS panel after setup: 1 Ready, 2 Reinstall](docs/images/readme/dlss-linux.png)

To install again later, click **Reinstall** (2) next to **Ready** to show both buttons.

## Reporting a problem

Open an [issue](https://github.com/tasarren/Lichii/issues) with the build number, the game, your
CPU, GPU and driver, your settings, and the log (File > Open Lichii Folders > Log Folder) or a Help > Report a Bug
file. Check it for personal information first. Do not upload games, keys or firmware. Bug
bundles, GPU traces, shader dumps, pipeline caches and crash dumps can contain game data: do not
attach them to public reports; ask a maintainer first.

## Building

See the [build guide](docs/Build.md).

## Credits and license

This fork builds on Lichii and the projects it comes from: Eglantine, Eden, yuzu and Sudachi, and
their contributors, including Eglantine's original developer Camille LaVey. Original copyright
notices and third-party licenses are kept. See [LICENSE.txt](LICENSE.txt) and the source files for
the license terms. Not affiliated with Nintendo.

## Support

This fork is maintained by [@tasarren](https://github.com/tasarren). Tip on [Ko-fi](https://ko-fi.com/tasarren) or sponsor on [GitHub](https://github.com/sponsors/tasarren).
