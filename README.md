# Objectify Entity
Helper library for objectifying the syntax when dealing with entities and their components.
This library was made for Noita mods.


## Install
To add this library to your mod:
- Copy `objectify.lua` and `vector2.lua` to somewhere in your mod.
- Edit `objectify.lua`'s `config` to point to where you placed `vector2.lua`


## Usage Examples
In any file in your mod, you can now request the library and deal with entities as objects.

For example in `init.lua`:

```lua
function OnPlayerSpawned(player_entity)
  dofile("my_mod/scripts/libs/objectify.lua")

  local player = objectify_entity(player_entity)

  -- fetch components
  local chardata = player.CharacterDataComponent

  -- fetch member of component:
  GamePrint(chardata.fly_recharge_spd)

  -- modify component (this will edit the chardata[1])
  chardata.fly_recharge_spd = 100

  -- dealing with multicomponents:
  local audio_components = player.AudioLoopComponent
  for _, comp in ipairs(audio_components) do
    GamePrint(comp.event_name)
  end
  -- or
  GamePrint(audio_components[1].event_name)

  -- vectors (handled with vector2 objects)
  -- chardata.vector is equivalent to chardata[1].vector
  chardata.vector.mVelocity = vector2(0, -100)
  GamePrint(tostring(chardata.vector.mVelocity))

  -- some values are MetaCustom values:
  local platforming = player.CharacterPlatformingComponent
  
  platforming.meta.run_velocity = 10
  GamePrint(platforming.meta.run_velocity)
  
  -- additionally, player[n] will fetch the n'th component of the player object.
end
```
