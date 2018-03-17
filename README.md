# OnlineHost

This bot serves three purposes: Rolling Dice, Proctoring Matches, and providing an archive for looking up old friends from AOL by screename searching.

Future features will probably be added, aswell.

## Status

OnlineHost is a work in progress.  Some of the features outlined here are not implemented yet but are in the planning stages.  Expect some volatility if you are an early adopter.  You've been warned.

## Usage

### Add To Your Server

[Invite the Bot to join your server.](https://discordapp.com/api/oauth2/authorize?client_id=392262179409231872&permissions=268454992&scope=bot)

### Rolling Dice
* `~roll` to roll 2 6-sided dice
* `~roll 2d20` to roll 2 20-sided dice
* `~roll 99d999` to roll 99 999-sided dice
* `~roll 4f` to roll 4 fate dice

Essentially, rolling anything from `1d2` to `99d999`.  Modifiers can be added by using `+#` or `-#`.  By default, however, only dice with `d20 to d100` will be scored as this is the traditional dice range for RhyDin.

#### Rolling on a "Table"
* `~choose item 1, item 2, ...` to roll 1dn, where n is the number of items in comma-separated list.

### Screen Name Database

* `~sn:list [@username]` Show the current user's archived screen names, or show the screen names of the provided user.
* `~sn:add sn1 [, sn2 [, ...]]` Add these screen names to the archive for the current user.  Use of this command is considered an opt-in for search.
* `~sn:remove sn1 [, sn2 [, ...]]` Remove these screen names from the archive for the current user.
* `~sn:search term[s]` Search screen names for the provided terms.  Adding screen names is considered an opt-in to being searched.  optout is available without needing to delete screen names.
* `~sn:optout` This command will prevent your screen names from being searchable.
* `~sn:opton` This command will re-enable your screen names to be found with search if you previously opted out.

### NumberWang

We have Round 1 of NumberWang: [NumberWang on Youtube](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=4&cad=rja&uact=8&ved=0ahUKEwiN0rDUosjYAhXIRSYKHSdxBtcQtwIIODAD&url=https%3A%2F%2Fwww.youtube.com%2Fwatch%3Fv%3DqjOZtWZ56lc&usg=AOvVaw2_iklaJ9EfSmeYhcxsUNRU)

* `~nw #` Play your number for NumberWang.
* `~nw:score` Show your score for NumberWang.
* `~nw:score @user` Show another user's score for NumberWang.
* `~nw:leaders` (future) Show the leaderboard for NumberWang.

### Zombie Game

Play a game of zombie die.

* `~brains` to join a game.
* `~brains` to start the game after 3+ people join (anyone can still join an active game).
* `~brains` to roll the dice when it's your turn.
* `~pass` to total your score and pass the dice to the next player.

### Admin Commands

There are administrative commands available, BUT they are not accessible to just anyone.  The Bot owner has perview to use any command anywhere the bot has been invited.  Server Owners will also have access to useful commands to help determine the bot's behavior on their server.

## Future Usage

The actual implementation of how the following commands will probably differ significantly from those proposed here.  This section represents mainly a thought dump on what could be done.

### Rolling Dice

* `~roll 4d6!` to roll exploding dice on thie highest side (6s in the example).
* `~roll 4d6!>4` to roll exploding dice on numbers greater than or equal to 4
* `~roll 4d6!<4` to roll exploding dice on numbers less than or equal to 4
* `~roll 4d6>5` to roll 4d6 and drop any rolls greater than or equal to 5
* `~roll 4d6<2` to roll 4d6 and drop any rolls less than or equal to 2

### Rolling on a "Table"

* `~choose tablename` Choose from a pre-compiled table
* `~settable tablename item 1, item 2, ...` Setup a tablename.  Channel admins can set tables that override server tables, server tables override global tables, and admin override-flagged tables will override everything.

### Proctoring Matches

* `~proctors:open` Allow anyone to proctor matches.
* `~proctors:closed` Allow only registered Proctors to proctor matches.
* `~proctors:add @username` Flag a user as allowed to proctor matches.
* `~proctors:remove @username` Remove a user from the proctors list.

* `~match:open [matchtype]` Proctors command to start a match.  Only one match can be open for init at a time in a channel, and a proctor may only proctor 1 match at a time globally.
* `~match:init` Players command to join an open match in the channel.  Rolls 1d100.
* `~match:begin` Proctor will close an open match, and set the turn order, and the first player may attack.  Tied init rolls much be broken first.
* `~match:roll [1-5]d[2-100] @username | 2:@username 2:@username` Rolling dice for a match will target the @user[s] for damage.
* `~match:scoreboard` Prints out a scoreboard for the current match.  If the proctor uses this command, it prints to the channel of the current match.  If a player uses this command, OnlineHost will send the scoreboard in a DM.  Anyone else will do nothing since they are not associated with a match.
* `~match:scoreboard @proctor` Prints out a scoreboard for the current match being run by the mentioned proctor. Scoreboard will be sent in a DM.
* `~match:scoreboard:update @username [+|-]?[1-100]` Proctor command to update scores if something got mixed up (like a forgotten modifier).
* `~match:remove @username [reason]` Proctor can remove a user for whatever reason.
* `~match:end` Proctor can end a match prematurely.
* `~match:remove @username` Proctor can remove a match player.
* `~match:assign @username` Proctor can hand a match over to another proctor if they need to leave.
* `~match:assign @proctor @username` Server or channel admin can forcefully reassign a match to another proctor.
* `~match:npc dice health [@proctor] NPC's Name` Create an NPC in the match.  Optionally, specify a "proctor" to play the NPC.

### Settings

* `~set channel:owner @username` Allows channel-related bot admin commands to be used by someone other than server owner, including adding channel admins.  If not set, the server owner is assumed to be the channel owner.
* `~set channel:admin @username` Server or channel owner can allow someone to manage channel-related bot settings.  Admins cannot add/remove admins.
* `~set channel:token "~"` Change the token used on a channel-by-channel basis.
* `~set channel:sleep` Tells bot to ignore events in the current channel. Only `~set channel:awake` will be available.
* `~set channel:awake` Tells bot to resume listening to events in the current channel if previously put to sleep.
* `~set scores <on|off>` Show scoring for roles according to score table.
* `~set scores:method <sum|table|function|default> [optional name for table or function]` set how dice are scored.
* `~set scores:table tablename` ... This is a secret.
