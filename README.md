[![](https://jitpack.io/v/Eisi05/NpcApi.svg)](https://jitpack.io/#Eisi05/NpcApi)

# NpcAPI

A powerful and easy-to-use NPC (Non-Player Character) API for Minecraft Spigot plugins that allows you to create, manage, and customize NPCs with
advanced features.

## Features

- 🎭 Create custom NPCs with ease
- 🎨 Customize NPC appearance (skins, glowing effects, etc.)
- 👆 Handle click events and interactions
- 🎬 Play animations and control NPC behavior
- 💾 Save and load NPCs persistently
- 👥 Show/hide NPCs for specific players
- 🔍 Comprehensive NPC management system

## Installation

### Maven

Add the following repository and dependency to your `pom.xml`:

```xml
<repository>
    <id>jitpack.io</id>
    <url>https://jitpack.io</url>
</repository>

<dependency>
    <groupId>com.github.Eisi05</groupId>
    <artifactId>NpcApi</artifactId>
    <version>1.0</version>
</dependency>
```

### Gradle

Add the following to your `build.gradle`:

```gradle
dependencyResolutionManagement {
    repositoriesMode.set(RepositoriesMode.FAIL_ON_PROJECT_REPOS)
    repositories {
        mavenCentral()
        maven { url 'https://jitpack.io' }
    }
}

dependencies {
    implementation 'com.github.Eisi05:NpcApi:Tag'
}
```

## Quick Start

### Plugin Setup

Initialize the NpcAPI in your plugin's main class:

```java

@Override
public void onEnable()
{
    // Initialize NpcAPI with default configuration
    NpcApi.createInstance(this, new NpcConfig());
}

@Override
public void onDisable()
{
    // Properly disable NpcAPI
    NpcApi.disable();
}
```

## Usage Examples

### Creating a Basic NPC

```java
// Create a location where the NPC should spawn
Location location = new Location(world, x, y, z);

// Create a new NPC with a name
NPC npc = new NPC(location, WrappedComponent.create("Test"));

// Enable the NPC to make it visible to all players
npc.setEnabled(true);
```

### Customizing NPC Appearance

```java
// Make the NPC glow with a red color
npc.setOption(NpcOption.GLOWING, ChatColor.RED);

// Set a custom skin from a player
npc.setOption(NpcOption.SKIN, Skin.fromPlayer(player));
```

### Handling Click Events

```java
// Set up a click event handler
npc.setClickEvent(event -> {
    Player player = event.getPlayer();
    NPC clickedNpc = event.getNpc();
    player.sendMessage("You clicked " + clickedNpc.getName().toLegacy());
});
```

### Managing NPC State

```java
npc.save();
npc.setName(WrappedComponent.create("New Name"));
npc.setLocation(newLocation);
npc.reload();
```

### Advanced NPC Control

```java
npc.playAnimation(/* animation parameters */);
npc.showNPCToPlayer(player);
npc.hideNpcFromPlayer(player);
npc.lookAtPlayer(player);
npc.delete();
```

## NPC Management

### Getting All NPCs

```java
// Get a list of all available NPCs
List<NPC> allNpcs = NpcManager.getList();
```

### Finding NPCs by UUID

```java
// Get a specific NPC by its UUID
UUID npcUuid = /* your NPC's UUID */;
NPC npc = NpcManager.fromUUID(npcUuid);
```

## API Reference

### NPC Class

| Method                                | Description                              |
|---------------------------------------|------------------------------------------|
| `setOption(NpcOption, Object)`        | Set NPC options like glowing, skin, etc. |
| `setClickEvent(Consumer<ClickEvent>)` | Set the click event handler              |
| `setEnabled(boolean)`                 | Enable/disable NPC visibility            |
| `save()`                              | Save NPC to persistent storage           |
| `reload()`                            | Reload NPC data                          |
| `setName(WrappedComponent)`           | Update NPC display name                  |
| `setLocation(Location)`               | Move NPC to new location                 |
| `playAnimation(...)`                  | Play NPC animation                       |
| `showNPCToPlayer(Player)`             | Show NPC to specific player              |
| `hideNpcFromPlayer(Player)`           | Hide NPC from specific player            |
| `lookAtPlayer(Player)`                | Make NPC look at player                  |
| `delete()`                            | Remove NPC permanently                   |

## Requirements

- Java 17+
- Spigot 1.17+ (compatible with newer versions)
- Minecraft server with NPC support
