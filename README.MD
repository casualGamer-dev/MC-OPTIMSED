# Minecraft server optimization guide

Note for users that are on vanilla, Fabric or Spigot (or anything below Paper) - go to your server.properties and change `sync-chunk-writes` to `false`. This option is forcibly set to false on Paper and its forks, but on other server implementations you need to switch this to false manually. This allows the server to save chunks off the main thread, lessening the load on the main tick loop.

Guide for version 1.19. Some things may still apply to 1.15 - 1.18.
# Intro
There will never be a specific ready made configuration that will give you perfect results. Each server has their own needs and limits on how much you can or are willing to sacrifice. Tinkering around with the options to fine tune them to your servers needs is what it's all about. This configs only aims to help you understand what options have impact on performance and what exactly they change. If you think you found inaccurate information within these configs, you're free to open an issue or set up a pull request to correct it.

# Server Performance Configs
Optimised configs aimed for big survival economy servers. That require handling a lot of players on a single server. But I highly recommend customising it for your needs using the guides listed below. 

## Server JAR
Your choice of server software can make a huge difference in performance and API possibilities. There are currently multiple viable popular server JARs, but there are also a few that you should stay away from for various reasons.

Recommended top picks:
* [Paper](https://github.com/PaperMC/Paper) - The most popular server software that aims to improve performance while fixing gameplay and mechanics inconsistencies.
* [Pufferfish](https://github.com/pufferfish-gg/Pufferfish) - Paper fork that aims to further improve server performance.
* [Purpur](https://github.com/PurpurMC/Purpur) - Pufferfish fork focused on features and the freedom of customization.

You should stay away from:
* Any paid server JAR that claims async anything - 99.99% chance of being a scam.
* Bukkit/CraftBukkit/Spigot - Extremely outdated in terms of performance compared to other server software you have access to.
* Any plugin/software that enables/disables/reloads plugins on runtime. 
* Many forks further downstream from Pufferfish or Purpur will encounter instability and other issues. If you're seeking more performance gains, optimize your server or invest in a personal private fork.
## Recommendations

### Stay away from these plugins
* **Stacker plugins** - stacking entities causes more lag because the server is than always trying to spawn new mobs. I would recommend stacker plugins only for stacking mobs from spawners and disabling their AI.
* **Item removal plugins** - these "free performance" plugins are most of the time useless as you can "replace" them with item/alt item despawn rates in spigot.yml.
* **Plugin managers** - Using plugins to reload other plugins without restarting the server, can cause glitches.

### Check your timings
Create a timings report, timings can give you a lot of helpful information about what is making your server lag ext.
join our [Discord](https://discord.gg/hCecZHaDkQ) if you require help with it
### Useful Plugins 
* [Insights](https://www.spigotmc.org/resources/insights-super-configurable-region-limits-asynchronous-scans-1-17-x.56489/) - Allows you to set storage, redstone, items limits to regions, chunks or islands on skyblock/oneblock servers. 

* [Aikar Flags](https://blog.airplane.gg/aikar-flags/) - Java startup flags, the best to run a minecraft server.

* [AntiRedstoneClock](https://www.spigotmc.org/resources/antiredstoneclock-worldguard-plotsquard-support-1-8-1-17.18557/) - Disables redstone clocks when your server TPS drops.

* [Spark](https://www.spigotmc.org/resources/antiredstoneclock-worldguard-plotsquard-support-1-8-1-17.18557/) - Allows you to analyse your servers CPU and memory usage.

* [Chunky](https://github.com/pop4959/Chunky) - Pre-generates chunks for better performance on survival servers.

### measuring performance

## mspt
Paper offers a `/mspt` command that will tell you how much time the server took to calculate recent ticks. If the first and second value you see are lower than 50, then congratulations! Your server is not lagging! If the third value is over 50 then it means there was at least 1 tick that took longer. That's completely normal and happens from time to time, so don't panic.

## Timings
Way to see what might be going on when your server is lagging are Timings. Timings is a tool that lets you see exactly what tasks are taking the longest. It's the most basic troubleshooting tool and if you ask for help regarding lag you will most likely be asked for your Timings. Timings is known to have a serious performance impact on servers, it's recommended to use the Spark plugin over Timings and use Purpur or Pufferfish to disable Timings all together.
<br>