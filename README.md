# PersonalRadarPlugin
Supplemental Material for the Customizable Personal Radar Plugin on the Unreal Marketplace

See the code itself for more documentation.
Most variables and classes have descriptions

ALSO, PLEASE SEE THE DEMO MAP!!!
/Script/Engine.World'/PersonalRadar/Maps/PersonalRadarDemoMap.PersonalRadarDemoMap'

# Feature Overview

Add a slick Personal Radar to your project and customize it to your liking!  

•	Customize the range, icons, background image, and player icon.

•	Set different rotation styles (around player or fixed rotation)

•	Customize Icon, Icon Color, Size of each item

•	Filter Icons by type (by default includes Military, Civilian, and Building filters)

•	Set any actor to represent the center point of the radar

•	Easily add any actor to the minimap by giving it a Minimap Component

•	Full control over when items are shown, removed, or updated on Radar.

•	Comes with a Demo Map showing use of the Plugin and some sample Icons you can use.

•	Clean and Simple Code customize to your liking!

There is no render target / scene capture, the radar is fully rendered with UMG alone, which may save on performance compared to other minimap / personal radar systems.

You have fine-tuned control over when and how icons update on the minimap.  The basic Minimap Component only updates on-demand (when you run a function on it), but it is easy to inherit and override.  To demonstrate this, one included BP child updates the location of its owning actor on tick, and another one does so only on BeginPlay.

Radar Widget can be customized.  It can rotate around player, or let the player rotate and stay in the center, or follow another actor that is not the player.
Contains C++ and Blueprint content, as well as some sample icons for minimap items.

# MinimapSubsystem

This subsystem holds an array of Minimap Components which have registered themselves to be on the map.

Has functions to return specific sets of Icons in the form of minimap components (e.g. within X range of Y location) as well as remove and edit minimap components.  

The Personal Radar Widget and Minimap Components both call into it.

# Minimap Component
When told to do so, this component registers itself with the Minimap Subsystem and gives information regarding the owning actor's transform and icon information.  It can be given data manually, and the icon info can be updated at runtime (e.g. change icon when a character dies, change color when someone picks up a flag, etc).

The default (native) component only updates when told to (by calling functions on it).  I recommend making BP child classes that do more specific things in line with the goals of your game.  As exmaples, 2 are included with the project: One that auto-updates at Begin-Play (adding its actor to the personal radar) and on that updates every tick (great for frequently moving objects like characters).  You can as specific as you want, e.g. only update when a character has moved.

# Personal Radar Widget
This widget taps into the Minimap Subsystem to display icons around the Center Actor.

Range is in Unreal Units (cm), anything within range of Center Actor shows up

If you wamt tp make major changes, I highly recommend copying it to your project files and making the changes on your own copy.  
If you are just making cosmetic changes, consider inheriting from the original.

The Center Actor can be set to any actor, it does not have to be the Player Pawn.

The Map can be set with several rotation options.  It can rotate around the player, spinning the icons around depending on which way player faces.
It can keep a fixed "north" based on a specified up direction variable, and show the center actor turning when the actor rotates.

When Icon scale is based on Actor scale ,icon side is multiplied by actor scale.

Apply filters to show only certain unit types here.  If you use filtering, make sure every minimap icon has the proper filter type set!

Overscan Variable: This is responsible for rendering things that are just beyond the range of the personal radar, so that items to not appear to pop in/out when they are at the edge of the radar (and therefore the edge eof range)
