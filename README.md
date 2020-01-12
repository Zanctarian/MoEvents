# Mo' Events!
Mo' Events is an upcoming API coded very strongly by myself for Spigot 1.8 through 1.15.1. This API allows you to use more events in Spigot that may not have existed before. The API itself will not be uploaded on GitHub due to me selling it. However, this ReadME will serve as a guide to use it.

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
- **PLAYER_AFK_THRESHOLD** (Change the delay (in seconds) until the server recognizes a player to be AFK.)
- **PLAYER_AFK_KICK_ENABLED** (Change if you want to enable/disable AFK kicking. This does call the PlayerAFKKickEvent.)
- **PLAYER_AFK_KICK_THRESHOLD** (Change the delay (in seconds) when the player gets kicked. The timer starts after the player becomes AFK.)
- **PLAYER_AFK_KICK_REASON** (Change the reason the player is kicked. You can do this in the kick event too, but this changes the default reason. Color codes are supported.)
- **PLAYER_AFK_PING_MESSAGE** (Enable/disable being non-afk for sending a message.)
- **PLAYER_AFK_PING_BLOCK_PLACE** (Enable/disable being non-afk for placing a block.)
- **PLAYER_AFK_PING_BLOCK_BREAK** (Enable/disable being non-afk for breaking a block.)
- **PLAYER_AFK_PING_INTERACTION** (Enable/disable being non-afk for clicking.)
- **PLAYER_AFK_PING_ITEM_DROP** (Enable/disable being non-afk for dropping an item.)
- **PLAYER_AFK_PING_INVENTORY_CLOSE** (Enable/disable being non-afk for closing an inventory.)
- **PLAYER_AFK_PING_INVENTORY_OPEN** (Enable/disable being non-afk for opening an inventory.)
- **PLAYER_MOVE_EVENT_REFRESH_RATE** (Adjust the refresh rate in ticks for the PlayerSyncMoveEvent.)

Settings can be changed at any time while the plugin is running, but the best place to put them if you want to change just the default values is in your onEnable. If you want to change settings, input this line after the API initialization:
```MoEvents.getSettings().set(EVENT_SETTING, VALUE);```

If you don't know what value each setting is designed for, refer to this guide or the built in JavaDoc:
- **PLAYER_AFK_THRESHOLD** -> Integer | ```Default Value: 180```
- **PLAYER_AFK_KICK_ENABLED** -> Boolean | ```Default Value: false```
- **PLAYER_AFK_KICK_THRESHOLD** -> Integer | ```Default Value: 60```
- **PLAYER_AFK_KICK_REASON** -> String | ```Default Value: "&cYou have been kicked for being AFK!"```
- **PLAYER_AFK_PING_MESSAGE** -> Boolean | ```Default Value: true```
- **PLAYER_AFK_PING_BLOCK_PLACE** -> Boolean | ```Default Value: true```
- **PLAYER_AFK_PING_BLOCK_BREAK** -> Boolean | ```Default Value: true```
- **PLAYER_AFK_PING_INTERACTION** -> Boolean | ```Default Value: true```
- **PLAYER_AFK_PING_ITEM_DROP** -> Boolean | ```Default Value: true```
- **PLAYER_AFK_PING_INVENTORY_CLOSE** -> Boolean | ```Default Value: true```
- **PLAYER_AFK_PING_INVENTORY_OPEN** -> Boolean | ```Default Value: true```
- **PLAYER_MOVE_EVENT_REFRESH_RATE** -> Integer/Long | ```Default Value: 1L```

For an example of changing some settings, here's an example onEnable:
```
public void onEnable() {
    //Initialize the API
    MoEvents.init(this);
    
    //Set afk delay to 1 minute (60 seconds)
    MoEvents.getSettings().set(MoEventsSettings.PLAYER_AFK_THRESHOLD, 60);
    
    //Enable AFK kicking
    MoEvents.getSettings().set(MoEventsSettings.PLAYER_AFK_KICK_ENABLED, true);
}
```

## List of Supported Events
This list will cover supported events and a basic description of them.

##

### PlayerAFKEvent
The event will be called if the player goes AFK. (Delay is configurable).

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```kickPlayer(String reason)```
Kick the afk player from the server. Color codes supported.

##

### PlayerAFKKickEvent (Cancellable)
The event will be called if the player gets kicked for being AFK. (Delay, enable/disable, and reason for kicking is configurable).

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```setReason(String reason)```
Set the reason for why the player got kicked. Color codes supported.

```String getReason()```
Get the reason for the player being kicked.

##

### PlayerRTKEvent
The event will be called if the player is not longer AFK.

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```int getSecondsAway()```
Get the amount of time the player was AFK.

##

### PlayerSyncMoveEvent (Cancellable)
The event will be called if the player moves. (Refresh rate IS configurable).

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

##

### PlayerEquipArmorEvent (Cancellable)
The event will be called if the player equips armor.

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```ArmorType getType()```
Get the type of armor the has been equipped. (Helmet/Chestplate/Leggings/Boots)

```ItemStack getArmorPiece()```
Get the armor that has been equipped.

```setArmorPiece(ItemStack armorPiece)```
Set the armor as the armor piece.

```EquipMethod getMethod()```
Get how the player equipped the armor.

##

### PlayerUnequipArmorEvent (Cancellable)
The event will be called if the player unequips armor.

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```ArmorType getType()```
Get the type of armor the has been unequipped. (Helmet/Chestplate/Leggings/Boots)

```ItemStack getArmorPiece()```
Get the armor that has been unequipped.

```setArmorPiece(ItemStack armorPiece)```
Set the armor as the armor piece.

```EquipMethod getMethod()```
Get how the player unequipped the armor.

##

### PlayerSwimEvent
This event will be called if the player is swimming. (It is not a toggle event).

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```Block getBlock()```
Get the water block the player is swimming in.

```setBlock(Material material)```
Set the block the player is swimming in.

```LiquidType getType()```
Get whether the block the player is swimming in is water, lava, or none.

##

### PlayerJumpEvent (Cancellable)
This event will be called if the player initiates a jump.

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

##

### PlayerCompleteJumpEvent
This event will be called if the player finished a jump. (Event will be ignored if PlayerJumpEvent is cancelled).

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

##

### PlayerFallEvent
This event will be called if the player falls. (It's cancelled automatically if the player is in a jump instance. A jump instance is included when flying until you land).

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```boolean doesTakeFallDamage()```
Check if the player could take fall damage. True by default.

```takeFallDamage(boolean isDamaged)```
Set if the player should take fall damage when they land.

##

### PlayerLandEvent
This event will be called if the player lands a fall. (Does not interfere with PlayerCompleteJumpEvent and does not trigger in a jump instance. If the fall event is set for the player to not take damage, the damage method will ignore it).

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```Location landedAt()```
Get the location where the player landed at.

```double damageTaken()```
Get how much damage the player took after falling.

```setDamageTaken(double damage)```
Set how much fall damage the player takes. It ignores the takeFallDamage(boolean isDamaged) method in PlayerFallEvent.

##

### PlayerPingChangeEvent
This event will be called if the player's ping changes.

#### Methods

```Player getPlayer()```
Get the player that triggered the event.

```int getOldPing()```
Get the player's ping before it changed.

```int getNewPing()```
Get the player's ping after it changed. (Their current ping).


##

### ServerTPSChangeEvent
This event will be called if the TPS on the server changes from the last known value. Max at 20.

#### Methods

```Server getServer()```
Get the server the plugin is running on.

```double getOldTPS()```
Get the TPS before the change.

```double getNewTPS()```
Get the TPS after the change (current TPS).

```double getOldTPSFormatted()```
Get the TPS before the change but rounded to the hundredths place.

```double getNewTPSFormatted()```
Get the TPS after the change (current TPS) but rounded to the hundredths place.

## Example Usage

```
public class Core extends JavaPlugin implements Listener {
  
    public void onEnable() {
        //Initialize the API
        MoEvents.init(this);
        
        //Set afk delay to 1 minute (60 seconds)
        MoEvents.getSettings().set(MoEventsSettings.PLAYER_AFK_THRESHOLD, 60);
        
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
    public void onRTK(PlayerRTKEvent e) {
      e.getPlayer().sendMessage("You are no longer AFK!");
    }
  
}
```
