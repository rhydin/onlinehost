# OnlineHost

This bot serves multiple purposes, most noteworthy are: Rolling Dice, Proctoring Matches, pseudo-private channels management, and providing an archive for looking up old friends from AOL by screename searching.  Other functionality can come or go depending on my availability to work on features.

## Status

OnlineHost is a work in progress.  Some of the features outlined here are not implemented yet but are in the planning stages.  Expect some volatility if you are an early adopter.  You've been warned.

## Getting Started

### Add To Your Server

[Invite the Bot to join your server.](https://discordapp.com/api/oauth2/authorize?client_id=392262179409231872&permissions=805334097&scope=bot)

If you are not the owner of the server, and you do not have the **Administrator** permission, you may not be able to grant all the necessary permissions for the bot to function.  If you find you do not see all the permissions (or at the very least the bolded permissions) from the following section listed on the bot invite authorization page, you will need to have the server owner or an administrator perform the authorization.

### Disclosure regarding required permissions

I hate it when an app demands all sorts of permissions, some of them not obvious what they are for, without any explanation.  In the interest of transparency and security as a first-principle of my development efforts here, I give you my reasons for requesting these permissions in my bot:

* **read_messages** Allows to bot to receive commands on the server
* **send_messages** Allows the bot to respond to commands on the server
* **manage_messages** Allows the bot to help keep the chat dialogue/backlog clear of excessive command usage
* **manage_channels** This is required for the Private Channels Module (bot must be able to create/remove channels)
* **manage_roles** This is required for the Private Channels Module (but must be able to create/remove roles, and apply them to users)

For future planned features (will update as features are implemented):
* create_instant_invite
* embed_links
* manage_webhooks
* add_reactions

If you want to explicitly exclude the bot from any channel, you can edit that channel's permissions to deny `Read Messages` to the bot's integrated role.

## Usage

### Bot Management

| Syntax | Description |
| --- | --- |
| `~token character` | Sets the command token for the current channel. |
| `~stoken character` | Sets the command token for the current server. |
| `~mute` | Bot will ignore the current channel. |
| `~unmute` | Bot will resume parsing commands in current channel. |
| `~help` | Lists commands available on the bot. |
| `~help command` | Shows the help document for the command, if one is present. |

#### Admin Commands

The Bot owner has several commands available, including global ban for when users abuse the Bot's functionality.  Anyone banned from using the bot for explicit abuse WILL NOT be unbanned. Anyone caught creating multiple accounts to circumvent this ban will be reported to Discord for abuse.

### Rolling Dice

| Syntax | Description |
| --- | --- |
| `~roll` | Rolls two 6-sided dice (default dice). |
| `~roll 2d20` | Rolls two 20-sided dice. |
| `~roll 99d999` | Rolls ninety-nine 999-sided dice. |
| `~roll 4f` | Rolls four fate dice. |

Essentially, rolling anything from `1d2` to `99d999`.  Modifiers can be added by using `+#` or `-#`.  By default, however, only dice with `d20 to d100` will be scored in the tradition of RhyDin scoring.  I may update the bot at a later date to allow server owners to define a custom table, but I will probably limit this feature to Patreon patrons.

#### Rolling Against a List

| Syntax | Description |
| --- | --- |
| `~choose item 1, item 2, ...` | Rolls `1dn`, where n is the number of items in comma-separated list. |

### Rolling on a Table

Roll tables are scoped to the server.  Server owners, server administrators, or users with the `Manage Server` permission can create/modify tables.

| Syntax | Description |
| --- | --- |
| `~choose tablename [(+/-)#]` | Choose from a pre-compiled table by name. Allows integer modifiers. |
| `~table new tablename [description]` | Create a table by name, optionally adding a description. |
| `~table list` | Show a list of available table names. |
| `~table info tablename` | Show the dice, description, and error information (such as gaps in the table sequence). |
| `~table add tablename item 1, item 2 [, ...]` | Add items to a table, 1 side per item. |
| `~table add tablename [s,e]item 1, [s,e]item 2 [, ...]` | Add items to a table, were `s` and `e` in square brackets represent the start and end sides for the item. |
| `~table rewrite tablename side-# new item value` | Rewrite the item with the side-# in it's range. |
| `~table remove tablename side-#` | remove an item from a table with the side-# in it's range. |
| `~table delete tablename` | Delete a table entirely. |

### "Private" or "Personal" Channels

| Syntax | Description |
| --- | --- |
| `~privatechannels` | If user is admin, DMs them information about channels. |
| <code>~privatechannels <on&#124;off></code> | Enables/Disables creation of private channels. |
| `~createchannel hyphenated-channel-name [topic]` | Users can create ONE private channel.  Any characters after the name become the channel's topic. |
| `~deletechannel` | Deletes the user's channel, or an admin can delete the current channel. |
| `~invite @user1 [@user2 ...]` | Adds @user(s) to your personal channel. |
| `~dismiss @user1 [@user2 ...]` | Removes @user(s) from your personal channel. |
| `~leave` | Remove yourself from the current personal channel. |

### Screen Name Database

| Syntax &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description |
| --- | --- |
| `~sn:list [@username]` | Show the current user's archived screen names, or show the screen names of the provided user. |
| `~sn:add sn1 [, sn2 [, ...]]` | Add these screen names to the archive for the current user.  Use of this command is considered an opt-in for search. |
| `~sn:remove sn1 [, sn2 [, ...]]` | Remove these screen names from the archive for the current user. |
| `~sn:search term[s]` | Search screen names for the provided terms.  Adding screen names is considered an opt-in to being searched.  optout is available without needing to delete screen names. |
| `~sn:optout` | This command will prevent your screen names from being searchable. |
| `~sn:optin` | This command will re-enable your screen names to be found with search if you previously opted out. |

### NumberWang

We have Round 1 of NumberWang (needs citation).  Scores will be reset when the bot is restarted.

| Syntax | Description |
| --- | --- |
| `~nw #` | Play your number for NumberWang. |
| `~nw:score` | Show your score for NumberWang. |
| `~nw:score @user` | Show another user's score for NumberWang. |
| `~nw:leaders` | (future) Show the leaderboard for NumberWang. |

### Eat Some Brains, do get Shot

Play a game of brain dice.

| Syntax | Description |
| --- | --- |
| `~brains join` | Join the current game. |
| `~brains start` | Start the game after 3+ people join (anyone can still join an active game). |
| `~brains roll` | Roll the dice on your turn. |
| `~brains pass` | Pass the dice to the next player. |
| `~brains scores` | Pass the dice to the next player. |
| `~brains take` | Take ownership of the game in this channel. |
| `~brains quit` | Leave a game before it's finished. |

## Future Usage (not implemented yet)

The actual implementation of how the following commands will probably differ significantly from those proposed here.  This section represents mainly a thought dump on what could be done.

### Rolling Dice

| Syntax | Description |
| --- | --- |
| `~roll 4d6!` | to roll exploding dice on thie highest side (6s in the example). |
| `~roll 4d6!>4` | to roll exploding dice on numbers greater than or equal to 4 |
| `~roll 4d6!<4` | to roll exploding dice on numbers less than or equal to 4 |
| `~roll 4d6>5` | to roll 4d6 and drop any rolls greater than or equal to 5 |
| `~roll 4d6<2` | to roll 4d6 and drop any rolls less than or equal to 2 |

### Proctoring Matches

#### Managing staff.

| Syntax | Description |
| --- | --- |
| `~proctors:open` | Allow anyone to proctor matches. |
| `~proctors:closed` | Allow only registered Proctors to proctor matches. |
| `~proctors:add @username` | Flag a user as allowed to proctor matches. |
| `~proctors:stats @username` | Show statistics for a proctor. |
| `~proctors:remove @username` | Remove a user from the proctors list. |

#### Running matches.

| Syntax | User | Description |
| --- | :---: | --- |
| `~match:open [matchtype]` | Proctor | Proctors command to start a match.  Only one match can be open for init at a time in a channel, and a proctor may only proctor 1 match at a time globally. |
| `~match:open singles @user1 @user2` | Proctor | Start a one-on-one match between @user1 and @user2. |
| `~match:open mass @user1 @user2 @user3 ...` | Proctor | Proctors command to start a mass spar with a closed list of conbatants. |
| `~match:open mass` | Proctor | Proctors command to start a mass spar open to anyone as conbatants. |
| `~match:init` | Player | Players command to join an open match in the channel.  Rolls 1d100. |
| `~match:begin` | Proctor| Proctor will close an open match, and set the turn order, and the first player may attack.  Tied init rolls much be broken first. |
| <code>~match:roll [1-5]d[2-100] @username &#124; 2:@username 2:@username</code> | Player | Rolling dice for a match will target the @user[s] for damage. |
| `~match:scoreboard` | Participants | Prints out a scoreboard for the current match.  If the proctor uses this command, it prints to the channel of the current match.  If a player uses this command, OnlineHost will send the scoreboard in a DM.  Anyone else will do nothing since they are not associated with a match. |
| `~match:scoreboard @proctor` | Anyone | Prints out a scoreboard for the current match being run by the mentioned proctor. Scoreboard will be sent in a DM. |
| <code>~match:scoreboard:update @username [+&#124;-]?[1-100]</code> | Proctor | Proctor command to update scores if something got mixed up (like a forgotten modifier). |
| `~match:leave [reason]` | Player | a Player can quit a match at any time for any reason or no reason. |
| `~match:remove @username [reason]` | Proctor | Proctor can remove a user for whatever reason. |
| `~match:end` | Proctor | Proctor can end a match prematurely. |
| `~match:remove @username` | Proctor | Proctor can remove a match player. |
| `~match:assign @username` | Proctor | Proctor can hand a match over to another proctor if they need to leave. |
| `~match:assign @proctor @username` | Admin | Server or channel admin can forcefully reassign a match to another proctor. |
| `~match:npc dice health [@proctor] NPC's Name` | Proctor | Create an NPC in the match.  Optionally, specify a "proctor" to play the NPC. |

### Settings (Administrative commands)

Not sure if any of these will be good.
* `~set channel:owner @username` Allows channel-related bot admin commands to be used by someone other than server owner, including adding channel admins.  If not set, the server owner is assumed to be the channel owner.
* `~set channel:admin @username` Server or channel owner can allow someone to manage channel-related bot settings.  Admins cannot add/remove admins.
* `~set [module] <on|off> [server|channel|@user]` Turn on/off specific functionality for a specified entity.
* `~set scores:method <sum|table|function|default> [optional name for table or function]` set how dice are scored.

## Getting Support

Issues can be opened here on Github, or you can reach out to me on my beta testing server at: https://discord.gg/t6k3EQZ
