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
}```
The variable "this" refers to the class JavaPlugin.

## API Settings
You heard it right, the API does have configurable settings to adjust it to your need. All the current available settings are:
- PLAYER_AFK_THESHOLD (Change the delay (in seconds) until the server recognizes a player to be AFK.)
- PLAYER_AFK_KICK_ENABLED (Change if you want to enable/disable AFK kicking. This does call the PlayerAFKKickEvent.)
- PLAYER_AFK_KICK_THESHOLD (Change the delay (in seconds) when the player gets kicked. The timer starts after the player becomes AFK.)
- PLAYER_AFK_KICK_REASON (Change the reason the player is kicked. You can do this in the kick event too, but this changes the default reason. Color codes are supported.)

Settings can be changed at any time while the plugin is running, but the best place to put them if you want to change just the default values is in your onEnable. If you want to change settings, input this line after the API initialization:
```MoEvents.getSettings().set(EVENT_SETTING, VALUE);```

If you don't know what value each setting is designed for, refer to this guide or the built in JavaDoc:
- PLAYER_AFK_THESHOLD -> Integer
- PLAYER_AFK_KICK_ENABLED -> Boolean
- PLAYER_AFK_KICK_THESHOLD -> Integer
- PLAYER_AFK_KICK_REASON -> String

For an example of changing some settings, here's an example onEnable:
```
public void onEnable() {
  //Initialize the API
  MoEvents.init(this);
  
  //Set afk delay to 1 minute (60 seconds)
  MoEvents.getSettings().set(MoEventsSettings.PLAYER_AFK_THESHOLD, 60);
  
  //Enable AFK kicking
  MoEvents.getSettings().set(MoEventsSettings.PLAYER_AFK_KICK_ENABLED, true);
}```

## List of Supported Events
- PlayerAFKEvent (If the player goes AFK)
- PlayerAFKKickEvent (If the player gets kicked for being AFK)
- PlayerRTKEvent (If the player returns to the keyboard (no longer AFK))
- PlayerSyncMoveEvent (A less laggier version of PlayerMoveEvent by putting it on a timer)

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
  public void onAFK(PlayerAFKEvent e)
  {
    e.getPlayer().sendMessage("You are now AFK!");
  }
  
  @EventHandler
  public void onRTK(PlayerRTKEvent e)
  {
    
  }
  
}
```
