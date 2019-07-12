# Teleport Request

[The Pixel Shadow](https://minetest.tv/) Minetest game servers have switched from "teleport" to "teleport request" via the *teleport-request* mod. This mod makes it so players must send a request to another player in order to teleport to them. Before they will be allowed to do so, the player must accept the request. This prevents malicious users from teleporting to players' private areas without their permission. It also enhances the overall privacy of our services since if denied teleport, a player must instead travel to the area and "use the front door" so to speak... which might be a locked iron door.

## Privileges:
Each command needs a privilege. These are the following privileges:
- **tp** is requiered in order to use all commands.
- **tp_tpc** is requiered in order to use "/tpc"
- **tp_tpc** is requiered in order to use "/tpe"
- **tp_tpc** is requiered in order to use "/tpj"
- **interact** is also requiered to use all commands.
"tp_admin" overrides everything: e.g. you can teleport to players even when they haven't decided if to accept, or not.
Players can also teleport to coordinates, however, if the area is protected, the teleport will be denied.

## Usage:

``` /tpr [playername] ```
- **Name:** Teleport Request
- **Description:** Requests permission to teleport to another player, where [playername] is their exact name.
- **Required Privileges:** "interact", "tp"
- **Example Usage:** */tpr RobbieF* - requests permission from RobbieF to teleport to them.
- **Notes:** Usernames are case-sensitive. If you have "tp_admin", you will immediately teleport to the specificed player.

``` /tphr [playername] ```
- **Name:** Teleport Here Request
- **Description:** Request permission to teleport another player to you.
- **Required Privileges:** "interact", "tp"
- **Example Usage:** /tphr RobbieF - requests RobbieF to teleport to you.
- **Notes:** Usernames are case-sensitive.

``` /tpc [x,y,z] ```
- **Name:** Teleport to Coordinates
- **Description:** Teleport to coordinates.
- **Required Privileges:** "interact", "tp_tpc", "tp"
- **Notes:** Honors area protection: if the area is protected, it must be owned by you in order to teleport to it (or you must have "areas" privilege in order to teleport to those coordinates).

``` /tpj [axis] [distance] ```
- **Name:** Teleport Jump
- **Description:** Teleport a specified distance along a single specified axis.
- **Required Privilege:** "interact", "tp", "tp_tpc"
- **Available Options for *axis*:** x, y, z
- **Example Usage:** '/tpj y 10' - teleport 10 nodes into the air.

``` /tpe ```
- **Name:** Teleport Evade
- **Description:** In a sticky situation? Evade your enemy by teleporting to several nearby coordinates in random pattern. There's no knowing where you'll end up.
- **Required Privileges:** "interact", "tp_tpc", "tp"
- **Example Usage:** '/tpe' - teleports you to a random number of random coordinates in an evasive pattern.

``` /tpy ```
- **Description:** Accept a user's request to teleport to you or teleport you to them (does not apply to those who have "tp_admin" privilege).

``` /tpn ```
- **Description:** Deny a user's request to teleport to your teleport you to them (does not apply to those who have "tp_admin" privilege).

## Notes:
Players with the 'tp_admin' privilege override all the required privileges above, except 'interact'.

## Dependencies
There are no dependencies.  
However, optional dependencies are:
- [areas](https://github.com/minetest-mods/areas)

## License
See license [here](https://github.com/ChaosWormz/teleport-request/blob/master/LICENSE.md).

## Contributors:
- [RobbieF](https://minetest.tv) | [GitHub](https://github.com/Cat5TV)
- [DonBatman](https://github.com/donbatman)
- [NathanS21](http://nathansalapat.com/)
- [ChaosWormz](https://github.com/ChaosWormz)
- Traxie21, the original creator of this mod (however, he/she does not have a GitHub account anymore).
- All those who contributed to the original mod (please see init.lua).

## Installation
- Unzip the archive, rename the folder to "tpr" (**without the quotes**) and
place it in ..minetest/mods/

- GNU/Linux: If you use a system-wide installation place
    it in ~/.minetest/mods/.

- If you only want this to be used in a single world, place
    the folder in ..worldmods/ in your world directory.

For further information or help, see:
https://wiki.minetest.net/Installing_Mods

## TODO:
- Make it so if a player attempts to teleport to coordinates within a protected area owned by another player, and that player is online, the owner receives a request to allow or deny the user from teleporting to their area.
- Assess value in changing all tpr-based chat commands to one global command such as /tp to reduce the chance of confusion between tps_admin and the original mod (and also make it so people don't have to remember so many commands).
- Create a better sound effect for teleport and apply it to all teleport methods (not just /tpc)
- Add a handful of coordinates which can be set in config and teleported to by anyone regardless of their protection status (eg., Spawn).
- Create a new function for the actual set_pos() to remove all the redundant code each time the player is moved and the sound played.
- Rewrite to place all chat commands into one single command much like how /teleport works.
- Add a [different] sound effect at the source coords when a TP takes place (so other players hear it when to teleport away).
- Make evade respect land: no teleporting inside land, but instead make sure player is standing on surface or in water.
