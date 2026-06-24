# Universal Vein Miner
A fork of [2008Choco's VeinMiner](https://github.com/2008Choco/VeinMiner)

This project is now archived as [2008Choco's VeinMiner](https://github.com/2008Choco/VeinMiner) support Folia using Folialib (no more longer dumb patch like me)

This Minecraft (Bukkit) plugin aims to recreate portablejim's popular Minecraft Forge mod, VeinMiner, for CraftBukkit and Spigot servers. Licensed under GPLv3, releases are made on GitHub to comply with this license. You are currently on the GitHub page for VeinMiner (for Bukkit). portablejim's VeinMiner (for Forge) repository may be found [here](https://github.com/portablejim/VeinMiner). You are welcome to fork this project and create a pull request or request features/report bugs through the issue tracker.

# Overview

Universal Vein Miner introduces a vanilla-friendly mechanic that allows players to instantly mine groups of adjacent blocks, saving nothing more than precious time. Groups of ores, large trees, vast crop fields, and more. Each tool can have its own configurable block list allowing for limitless possibilities. This is a fantastic perk for Prison, Factions and Semi-Vanilla servers that isn't overpowered but still gives players a rewarding benefit for donating to your server.

![Universal Vein Miner in action](https://proxy.spigotmc.org/916cb079b12e62ff56589b0b9d54c253f273d668/68747470733a2f2f692e696d6775722e636f6d2f5a56724a7631422e676966)

## Features In Brief:
- Efficient mining of similar blocks in quick succession
- Powerful configuration for custom tool categories and block lists
- A variety of mining patterns to mine cubic regions, tunnels, or staircases
- Optional economy support
- Optional client-sided mod for custom keybinds
- A developer API for custom mining patterns and behaviors
- Drag-and-drop installation with no additional steps for server owners by default
- Native Anti Cheat and PlaceholderAPI support

## Client Companion Mod (Currently incompatible with Folia version of plugin)

The companion mod is an optional client-sided mod to provide a more rich user-experience for players including support for custom keybinds, keybinds for pattern switching, and vein mining wire frame rendering. This can be downloaded and installed for Fabric clients.

![Optional companion mod for Fabric](https://proxy.spigotmc.org/ce3961dfd358c5dcad00cdd34ea4941b35ceb553/68747470733a2f2f692e696d6775722e636f6d2f4c757065314b6b2e676966)

# Commands:
- `/veinminer ...`
  - `/veinminer reload`
    - Reload the `config.yml` and `categories.yml` and apply any changes you've made in the file  
    - **Permission:** `veinminer.command.reload`
  - `/veinminer version`
    - View version and developer information about VeinMiner
  - `/veinminer toggle [tool]`
    - Enable or disable vein mining  
    - If provided, toggle a specific tool  
    - **Permission:** `veinminer.command.toggle`
  - `/veinminer mode <mode>`
    - Change the way vein mining should be activated  
    - To use `"client"`, the VeinMiner Companion Mod must be installed on your client  
    - **Permission:** `veinminer.command.mode`
  - `/veinminer pattern <pattern>`
    - Change the way vein mining will search for and break blocks  
    - Patterns may be registered by add-ons, but VeinMiner provides:
      - `default`
      - `tunnel`
      - `staircase_up`
      - `staircase_down`
    - **Permission:** `veinminer.command.pattern`
  - `/veinminer givetool <category> <tool> [amount]`
    - Give yourself a tool from the given category (useful for tools with NBT)  
    - **Permission:** `veinminer.command.givetool`
  - `/veinminer import`
    - A tool for VeinMiner versions prior to 2.0.0 to import legacy JSON data into the new SQLite format  
    - **Permission:** `veinminer.command.import`
  - `/veinminer blocklist ...`
    - Mirrors `/blocklist` below
  - `/veinminer toollist ...`
    - Mirrors `/toollist` below

- `/blocklist ...`
  - `/blocklist <category> add <block>`
    - Add a vein mineable block to the given category  
    - Blocks can be Universal ids like `minecraft:stone`, or with states like `minecraft:chest[waterlogged=true]`  
    - **Permission:** `veinminer.command.blocklist`
  - `/blocklist <category> remove <block>`
    - Remove a block from the given category  
    - Blocks can be Universal ids like `minecraft:stone`, or with states like `minecraft:chest[waterlogged=true]`  
    - **Permission:** `veinminer.command.blocklist`
  - `/blocklist <category> list`
    - List all blocks (and block states) that are vein mineable with the given category  
    - **Permission:** `veinminer.command.blocklist`

- `/toollist ...`
  - `/toollist <category> add <item>`
    - Add an item to the given category's tool list  
    - **Permission:** `veinminer.command.toollist`
  - `/toollist <category> remove <item>`
    - Remove an item from the given category's tool list  
    - **Permission:** `veinminer.command.toollist`
  - `/toollist <category> list`
    - List all items useable for the given category  
    - **Permission:** `veinminer.command.toollist`

# Supported Anti Cheats

Universal Vein Miner natively supports many popular anti cheats so that your players will not be flagged with "fast break" (or whatever the equivalent flag is for your anti cheat of choice). If the anti cheat you are using is not listed here, there is a high chance that players using vein miner will be false flagged for breaking blocks too quickly. If you want another anti cheat added to this list, please request it be supported either in the Discussion Thread, on Discord, or on GitHub as an issue.
- AAC (Advanced AntiCheat) 5.x
- AntiAura
- FoxAddition (via their plugin)
- Grim Anti Cheat 2.3.59+
- LightAntiCheat
- Matrix 6.x+
- Negativity
- NoCheatPlus
- Spartan
- Themis
- Vulcan
  - Vulcan has a config option to enable the API, which is disabled by default. enable-api must be true

# Placeholders (PlaceholderAPI)

Universal Vein Miner happily supports PlaceholderAPI with the following placeholders:

- `"%veinminer_enabled%"`  
  Whether or not VeinMiner is toggled on.

- `"%veinminer_enabled_<category>%"`  
  Whether or not VeinMiner is toggled on for a given category.

- `"%veinminer_active%"`  
  Whether or not VeinMiner is active (e.g. the player has the keybind pressed).

- `"%veinminer_vein_mining%"`  
  `"true"` or `"false"` depending on whether or not the player is currently vein mining.  
  Only `"true"` for a brief moment in time.

- `"%veinminer_vein_mineable%"`  
  Provides `"true"` if the player's target block is vein mineable with the tool in hand, or `"false"` otherwise.  
  Requires player.

- `"%veinminer_vein_mineable_<category>%"`  
  Provides `"true"` if the player's target block is vein mineable with the specified category, or `"false"` otherwise.  
  Requires player.

- `"%veinminer_using_client_mod%"`  
  `"true"` or `"false"` depending on whether or not the player is using the client mod.

- `"%veinminer_pattern%"`  
  The key of the player's selected vein mining pattern.

- `"%veinminer_activation_strategy%"`  
  The name of the player's selected method of activation (`"Sneak"`, `"Client"`, `"Always"`, etc.).

- `"%veinminer_category%"`  
  Provides the name of the category of the tool in the player's hand.  
  Requires player.

- `"%veinminer_cost%"`  
  Provides the cost of vein mining.  
  - If a player is specified, provides the cost of the tool in the player's main hand (or the globally configured cost if no category is in hand), accounting for the `"free economy"` permission.  
  - If a player is **not** specified, provides the globally configured cost.

- `"%veinminer_cost_<category>%"`  
  Provides the cost of vein mining for the specified category.  
  - If a player is specified, accounts for the `"free economy"` permission.

- `"%veinminer_max_vein_size%"`  
  Provides the maximum amount of blocks mineable in a single vein mine.  
  - If a player is specified, provides the max vein size of the tool in the player's main hand (or the globally configured max vein size if no category is in hand).  
  - If a player is **not** specified, provides the globally configured max vein size.

- `"%veinminer_max_vein_size_<category>%"`  
  Provides the max vein size of the specified category.


# Messaging Protocol

Universal Vein Miner communicates with the Minecraft client via its [custom payload packet](https://wiki.vg/Protocol#Plugin_Message_.28clientbound.29). While VeinMiner does have its own client-sided companion mod, other client mods are capable of listening to these channels and intercepting messages. Additionally, while VeinMiner supplies API to communicate with the client, servers also have the option of listening to the raw message contents.
