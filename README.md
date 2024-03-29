**On account of discord's latest set of changes, OnlineHost is actually currently under the process of being rebuilt to transition from tokenized commands as described herein to slash commands.  Additionally, menus and reaction-based "control panels" will be transition to component-based (REAL BUTTONS!!!) functionality.  Have a nice day!**

# OnlineHost

This bot serves multiple purposes, most noteworthy are: Rolling Dice, Proctoring Matches, pseudo-private channels management, and providing an archive for looking up old friends from AOL by screename searching.  Other functionality can come or go depending on my availability to work on features.

## Status

OnlineHost is a work in progress.  Some of the features outlined here are not implemented yet but are in the planning stages.  Expect some volatility if you are an early adopter.  You've been warned.

## Disclosure

Per Discord's Developer Terms of Service (TOS), this bot does not log chat history.  Every possible effort is made to make good faith adherence to all TOS and any missed or misinterpreted terms will be rectified immediately.  The bot stores very little user data and only for operational purposes to ensure a stable, enjoyable experience for those wishing to engage with the bot.  The bot does store operational logs for quality control purposes, but those logs only consist of commands issued directly to the bot and other operating conditions.

## Getting Started

### Add To Your Server

[Invite the Bot to join your server.](https://discordapp.com/api/oauth2/authorize?client_id=392262179409231872&permissions=805334097&scope=bot)

If you are not the owner of the server, and you do not have the **Administrator** permission, you may not be able to grant all the necessary permissions for the bot to function.  If you do not have **manage_server** you cannot add bots at all.  If you find you do not see all the permissions enabled (or at the very least the bolded permissions) from the following section listed on the bot invite authorization page, you will need to have the server owner or an administrator perform the authorization.

### Disclosure regarding required permissions

I hate it when an app demands all sorts of permissions, some of them not obvious what they are for, without any explanation.  In the interest of transparency and security as a first-principle of my development efforts here, I give you my reasons for requesting these permissions in my bot:

* **read_messages** Allows to bot to receive commands on the server
* **send_messages** Allows the bot to respond to commands on the server
* **manage_messages** Allows the bot to help keep the chat dialogue/backlog clear of excessive command usage
* **manage_channels** This is required for the Private Channels Module (bot must be able to create/remove channels)
* **manage_roles** This is required for the Private Channels Module and Greeting Role assignment (bot must be able to assign roles to users)

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

### Greetings

#### Greeting Message

The bot can be configured to greet newcomers to your server with a custom message.
TODO

#### Greeting Role

The bot can be configured to assign a role to newcomers on your server.
TODO

### Rolling Dice

(The `~roll` command can be shortened to just `~r`.)

| Syntax | Description |
| --- | --- |
| `~roll` | Rolls two 6-sided dice (or whatever other default dice are set). |
| `~roll 2d20` | Rolls two 20-sided dice. |
| `~roll 99d999` | Rolls ninety-nine 999-sided dice. |
| Exploding Dice ||
| `~roll 4d6!` | to roll exploding dice on thie highest side (6s in the example). |
| `~roll 4d6!6` | to roll exploding dice on all 6s |
| `~roll 4d6!>4` | to roll exploding dice on numbers greater than 4 |
| `~roll 4d6!<3` | to roll exploding dice on numbers less than 3 |
| `~roll 4d10!>=4` | to roll exploding dice on numbers greater than or equal to 4 |
| `~roll 4d10!<=3` | to roll exploding dice on numbers less than or equal to 3 |
| Keep/Drop ||
| `~roll 4d6k` | to roll 4d6 and keep the highest die |
| `~roll 4d6d` | to roll 4d6 and drop the highest die (yes, drop the HIGHEST) |
| `~roll 4d6k3` | to roll 4d6 and keep the highest 3 rolls |
| `~roll 4d6d3` | to roll 4d6 and drop the highest 3 rolls (yes, drop the HIGHEST) |
| Success Counting ||
| `~roll 4d6c` | Counts the number of dice equal to the highest side (d6 = 6) |
| `~roll 4d10c>=4` | count the dice with sides greater than or equal to 4 |
| `~roll 4d10c<=3` | count the dice with sides less than or equal to 3 |
| Success Dice ||
| `~roll dh50` | to roll degrees of success against a target of 50; above = fail, below = success |
| Fudge Dice ||
| `~roll 4f` | Rolls four fudge dice. |
| Variables ||
| `~roll $(variable_name)` | Enclosing the variable name in `$(` and `)` to interpolate it |

Essentially, rolling anything from `1d2` to `99d999`.  Modifiers can be added by using `+#` or `-#`.  By default, however, only dice with `d20 to d100` will be scored in the tradition of RhyDin scoring.  I may update the bot at a later date to allow server owners to define a custom table, but I will probably limit this feature to Patreon patrons.

### User-defined Variables

OnlineHost has the capability of storing variables (abilities, statistics, characteristics, predefined roll strings, etc.).  These can either be stored against a channel or portably in a variable profile.

#### Variables

Variables can be nested.  Roll strings can be variablized.

| Syntax | Description |
| --- | --- |
| `~myvars` | Show a list of all set variables |
| `~myvars <var_name>` | Show the value of a variable, if it exists |
| `~myvars <var_name> <value of variable>` | Set the value of a variable |
| `~bulkvars <dictionary>` | Create multiple variables from a semicolon (`;`) separated list of `variable:value` pairs |
| `~delvars <var_name_1> [...]` | Delete one or more variables |

#### Profiles

| Syntax | Description |
| --- | --- |
| `~profile` | Reports which profile is current active |
| `~profile list` | List your profiles and reports how many variables and a brief description |
| `~profile create <profile_name> [optional profile description` | Make a new profile |
| `~use <profile_name>` | choose which profile is active in the current channel |
| `~rename <old_profile> <new_profile>` | change the name of an existing profile |
| `~copy <var> [from] <profile_1> [to] <profile_2>` | copy a variable from one profile to another |
| `~copyall <source_profile> <target_profile>` | copy all variables from one profile to another `see ~help profile:copyall for more` |
| `~merge <receiving_profile> <disposed_profile> [...]` | combine all the variables of two or more profiles into one |
| `~delete <profile_name>` | completely delete a profile and all it's contained variables |

### Rolling on a Set of Choices

#### Rolling Against an Impromptu List

| Syntax | Description |
| --- | --- |
| `~choose item 1, item 2, ...` | Rolls `1dn`, where n is the number of items in comma-separated list. |

#### Rolling Against a Predefined List

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

### Sparring Matches

| Syntax | User | Description |
| --- | :---: | --- |
| `~spar:open [fixed dice] [fixed hp]` | Proctor | Proctors command to start a match.  If fixed dice or fixed hp are provided, all participants will have the same dice or hp. |
| `~spar:join` | Player | Players command to join an open match in the channel.  Rolls 1d100. |
| `~spar:close` | Player | Closes the match to new participants and resolves any tiebreaking for initial rolls. |
| `~spar:begin` | Proctor | The combat is now ready for combat; the first player may attack. |
| `~spar:pause` | Proctor | Pauses a match preventing any commands for the match from being processed. |
| `~spar:resume` | Proctor | Start up a paused match. |
| <code>~spar:roll [1-5]d[2-100] @username &#124; 2 @username 2 @username</code> | Player | Rolling dice for a match will target the @user[s] for damage. |
| `~spar:scoreboard` | Participants | Prints out a scoreboard for the current match.  If the proctor uses this command, it prints to the channel of the current match.  If a player uses this command, OnlineHost will send the scoreboard in a DM. |
| `~spar:scoreboard @proctor` | Anyone | Prints out a scoreboard for the current match being run by the mentioned proctor. Scoreboard will be sent in a DM. |
| <code>~spar:update [hp dice maxhp init damage] @username [+&#124;-]?[1-100]</code> | Proctor | Proctor command to update player data if something got mixed up (like a forgotten modifier). |
| `~spar:quit [reason]` | Player | a Player can quit a match at any time for any reason or no reason. |
| `~spar:skip` | Proctor | Proctor can skip the current player's turn. |
| `~spar:add @username [dice]` | Proctor | Proctor can add a user after the match is started. |
| `~spar:remove @username [reason]` | Proctor | Proctor can remove a user for whatever reason. |
| `~spar:cancel` | Proctor | Proctor can end a match prematurely. |
| `~spar:remove @username` | Proctor | Proctor can remove a match player. |
| `~spar:assign @username` | Proctor | Proctor can hand a match over to another proctor if they need to leave. |
| `~spar:end` | Proctor | Proctor wraps up the match. This will tally xp (future feature) and removes the scoreboard. |

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

## Future Usage (not implemented yet)

The actual implementation of how the following commands will probably differ significantly from those proposed here.  This section represents mainly a thought dump on what could be done.

### Proctoring Matches

#### New functionality

| Syntax | User | Description |
| --- | :---: | --- |
| `~spar:assign @proctor @username` | Admin | Server or channel admin can forcefully reassign a match to another proctor. |
| `~spar:npc dice health [@proctor] NPC's Name` | Proctor | Create an NPC in the match.  Optionally, specify a "proctor" to play the NPC. |

#### Managing staff

| Syntax | Description |
| --- | --- |
| `~proctors:open` | Allow anyone to proctor matches. |
| `~proctors:closed` | Allow only registered Proctors to proctor matches. |
| `~proctors:add @username` | Flag a user as allowed to proctor matches. |
| `~proctors:stats @username` | Show statistics for a proctor. |
| `~proctors:remove @username` | Remove a user from the proctors list. |

### Settings (Administrative commands)

Not sure if any of these will be good.
* `~set channel:owner @username` Allows channel-related bot admin commands to be used by someone other than server owner, including adding channel admins.  If not set, the server owner is assumed to be the channel owner.
* `~set channel:admin @username` Server or channel owner can allow someone to manage channel-related bot settings.  Admins cannot add/remove admins.
* `~set [module] <on|off> [server|channel|@user]` Turn on/off specific functionality for a specified entity.
* `~set scores:method <sum|table|function|default> [optional name for table or function]` set how dice are scored.

## Getting Support

Issues can be opened here on Github, or you can reach out to me on my beta testing server at: https://discord.gg/t6k3EQZ

### Disclaimer and No Liability

The bot is neither created nor endorsed by Discord.  Any functionality is provided at the discretion of the bot's maintainer(s).  The Bot is operated as-is and makes no warranty to the quality of service.  Speak with your server owner if you have problems with the bot being present on any server.  Per Discord developer ToS, this bot does not make and store a record any chat. The bot only maintains logs of commands directly issued to it for security and maintenance purposes.
