# MoEvents
Mo' Events is an upcoming API coded very strongly by myself. This API allows you to use more events in Spigot that may not have existed before. The API itself will not be uploaded on GitHub due to me selling it. However, this ReadME will serve as a guide to use it.

## How to Acquire the API
In order to acquire the API, you must buy it through me. Currently, it's not available for sale as it's being worked on. However, when it is, this documentation will be updated with instructions.

## Getting Started
To get started with using this API, you must first add it to your library. You can either import an external jar or use maven to import it. When you buy the jar, you'll have access to the maven information with the jar download. The source code is provided with the jar as well so you can simply read the pom.xml too. 

Once you got the jar imported and ready to go, you only need to add one line to initialize the API. In your onEnable, use this:
```MoEvents.init(this);```
so that will look something like..
```
public void onEnable() {
    MoEvents.init(this);
}
```
The variable "this" refers to the class JavaPlugin.

## API Settings
You heard it right, the API does have configurable settings to adjust it to your need. All the current available settings are:
- **PLAYER_AFK_THESHOLD** (Change the delay (in seconds) until the server recognizes a player to be AFK.)
- **PLAYER_AFK_KICK_ENABLED** (Change if you want to enable/disable AFK kicking. This does call the PlayerAFKKickEvent.)
- **PLAYER_AFK_KICK_THESHOLD** (Change the delay (in seconds) when the player gets kicked. The timer starts after the player becomes AFK.)
- **PLAYER_AFK_KICK_REASON** (Change the reason the player is kicked. You can do this in the kick event too, but this changes the default reason. Color codes are supported.)

Settings can be changed at any time while the plugin is running, but the best place to put them if you want to change just the default values is in your onEnable. If you want to change settings, input this line after the API initialization:
```MoEvents.getSettings().set(EVENT_SETTING, VALUE);```

If you don't know what value each setting is designed for, refer to this guide or the built in JavaDoc:
- **PLAYER_AFK_THESHOLD** -> Integer
- **PLAYER_AFK_KICK_ENABLED** -> Boolean
- **PLAYER_AFK_KICK_THESHOLD** -> Integer
- **PLAYER_AFK_KICK_REASON** -> String

For an example of changing some settings, here's an example onEnable:
```
public void onEnable() {
    //Initialize the API
    MoEvents.init(this);
    
    //Set afk delay to 1 minute (60 seconds)
    MoEvents.getSettings().set(MoEventsSettings.PLAYER_AFK_THESHOLD, 60);
    
    //Enable AFK kicking
    MoEvents.getSettings().set(MoEventsSettings.PLAYER_AFK_KICK_ENABLED, true);
}
```

## List of Supported Events
This list will cover supported events and a basic description of them.

### PlayerAFKEvent
The event will be called if the player goes AFK. (Delay is configurable).

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```kickPlayer(String reason)```
Kick the afk player from the server. Color codes supported.

### PlayerAFKKickEvent
The event will be called if the player gets kicked for being AFK. (Delay, enable/disable, and reason for kicking is configurable).

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```setReason(String reason)```
Set the reason for why the player got kicked. Color codes supported.

```String getReason()```
Get the reason for the player being kicked.

```setCancelled(boolean cancel)```
Cancel the player from being kicked.

```isCancelled()```
Check if the event is cancelled.

### PlayerRTKEvent
The event will be called if the player is not longer AFK.

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```int getSecondsAway()```
Get the amount of time the player was AFK.

### PlayerSyncMoveEvent
The event will be called if the player moves. (Refresh rate WILL be configurable).

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```Location getOldLocation()```
Get the last location of the player before they moved.

```Location getNewLocation()```
Get the player's current location.

```Location getLocationDifference()```
Get the difference between the old and new locations. (Example: If a player moved 1 block on the x axis, but not on the Y or Z. The coordinates will be 1,0,0).

```teleportPlayer(Location location)```
```teleportPlayer(double x, double y, double z)```
```teleportPlayer(double x, double y, double z, float pitch, float yaw)```
Teleport the player to set position in the same world on move.

## Example Usage

```
public class Core extends JavaPlugin implements Listener {
  
    public void onEnable() {
        //Initialize the API
        MoEvents.init(this);
        
        //Set afk delay to 1 minute (60 seconds)
        MoEvents.getSettings().set(MoEventsSettings.PLAYER_AFK_THESHOLD, 60);
        
        //Enable AFK kicking
        MoEvents.getSettings().set(MoEventsSettings.PLAYER_AFK_KICK_ENABLED, true);
    
        //Change the kick reason
        MoEvents.getSettings().set(MoEventsSettings.PLAYER_AFK_KICK_REASON, "&cKicked due to being AFK!");
        
        //Register listener
        getServer().getPluginManager().registerEvents(this, this);
    }
      
    @EventHandler
    public void onAFK(PlayerAFKEvent e) {
        e.getPlayer().sendMessage("You are now AFK!");
    }
      
    @EventHandler
    public void onRTK(PlayerRTKEvent e)
    {
      e.getPlayer().sendMessage("You are no longer AFK!");
    }
  
}
```
