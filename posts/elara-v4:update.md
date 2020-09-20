# **Elara version 4 Update!**

## Event Logging Changes

### Notes

1) Logging now requires 2 permissions: `View Audit Logs, Manage Webhooks` - If the bot doesn't have those two permissions it won't log anything!
2) An add-on to the first one, the bot switched to webhook logging, but the bot itself doesn't store the webhook URLs. Instead it uses the channel IDs then fetches a webhook in the channel and uses that. (it doesn't get stored in a database)
3) The bot no longer stores messages in memory, that has been switched to the database, the message will be stored up to 2-3 days then it will be deleted from the database (if they wasn't deleted already): Note: The message content is encrypted using (aes256) encryption.
4) If the channel no longer exists, missing permissions/access, it will now clear that setting from that database to avoid erroring out a ton. Which means you'll have to setup that feature AGAIN (there isn't a good way to notify Admins about the issue so it will just reset it and move on)
5) If you want the bot to log emojis in messages you NEED to have `External Emojis` permission for the `@everyone` role!
6) For the auto-reactions for suggestions it now has a 10s cooldown and there is a setting to add ignore-roles, so it doesn't react to users with that role(s)
7) Welcome/Leave channels (logging) now requires (`Manage Server`) permission (to view and log invites that the member used when joining the server)
8) Suggestion reactions now require: `Add Reactions` and `Use External Emojis` permissions. 


## Added Events
1) `inviteCreate`: This will show when a member creates an invite.
2) `inviteDelete`: This will show when a member deletes an invite, or the invite expires on its own.

## Updated Events
Just about ALL events was updated, to either support the new logging format or better logging messages.
1) `guildMemberAdd`: Added an embed with the invite tracker (invite information) that the user joined with.
2) `userUpdate`: This was updated to post 1 message rather than 2 (since webhooks you can do multiple embeds within one message)
3) `messageUpdate, messageDelete, messageDeleteBulk`: Updated to the new message logging system (more info in notes)

## Removed
1) `owner.ignore` setting for auto suggestion reactions, replace by suggest: `ignore-roles`




# Commands Changes
### Notes
1) If you use the `currency/coin` commands, you WILL need to enable it again, use: `toggle currency` to do that. (NOTE: After 1-2 weeks the update goes out and the currency commands are disabled ALL of the currency-databases will be REMOVED from the database, to avoid storing data that isn't used)
2) For the command-ignore roles BE CAREFUL, if the user doesn't have `Manage Server` permission it will completely ignore them!
3) For action-logs the bot will require `Manage Webhooks` to log the actions, this inlcudes but not limited to: `ban, unban, kick, mute, unmute, warn, softban`
4) For reports & vclogs the bot will require: `Manage Webhooks` and `View Audit Logs` (vclogs only)
5) If you want the bot to delete the command prompts and the responses to the prompts use: `toggle prompts`

## Commands: Added
1) `crime` | You can now commit a crime! (Admins can set the success and failed replies aswell)
2) `ignore [member/role/channel] [type] [@role/@user/#channel]` | This will ignore a member, role or channel for the type you choose.
3) `crimes [type] [message]` | This allows the server admins to configure the crime commands.
4) `lyrics [song]` | Shows lyrics for a song you choose.
5) `color (#hex_color)` | Shows the color?, if there isn't any provided then it will show a random one.
6) `team [role_name]` | Assignable roles was added, it also supports user-profile badges (minus: the nitro and server boost badges, due to Discord)
7) `create` | This will create your currency database entry, it no longer auto creates it.
8) `roulette [amount] (space)` | Play the roulette game, note: If there is no space provided it will just show the roulette board.
9) `changemymind [text]` or `cmm [text]` | It's like the admire and wasted commands.
10) `slap [@user]` | It's like the admire/wasted commands.
11) `botlist [site] (@user)` | Look up information for a bot or user on the botlist you choose.
12) `bird/birb` | Shows an image of a bird
13) `cc [type] [?command_name] [?message_response]` | Confiruation for the custom commands.
14) `remindme [time] [message]` | Sets a reminder for you. (shortcut to the `reminders add time message` command)
15) `reminders [type] (time/ID) (message)` | Manage your reminders, or set new ones. 
16) `button` | Play will you press the button game (locked to NSFW marked channels, due to what could be returned)
17) `booplb/blb (page)` | Boops now have a leaderboard!, also if you don't wish to have your name listed there, use: `custom optout.boopslb`
18) `muted/mutes (@user/id or --all)` | Shows everyone currently muted or a certain user's muted information.
19) `react [message_url] (emoji) (amount)` | You can now pull random users from a reaction on a message! 

## Commands: Updated
1) `daily (@user)` | This now supports (`@user`) this will give your daily bonus to the user you mention.
2) `pay` | This now requires your currency DB entry to be at least an hour old (same as the daily command)
3) `deposit, withdraw, rob` | The embed was upodated and most of the currency commands now support: `all` and `half`
4) `work` | Updated the embed to look better/give more information.
5) `rob` | Without a member provided it will select a random one from the server.
6) `gif/giphy` Only works in NSFW marked channels, due to what could be returned. (also shows more information now.)
7) `reddit` | Updated the format for the embed.
8) `role` | It now works with multiple members provided: `role @role/id @member @member @member`
9) `profile` | You can now link your social media accounts to your Discord profile, and the embed was updated a bit.
10) `custom` | This now allows you to set your time, description, banner and social media links.
11) `adcheck/check` | Now supports `any` and `search` types (Any will look for ANY URLs in the members statuses, SEARCH: Allows you to search for anything in member statuses)
12) `serverinfo` | Updated the look of the embed and removed the member-status information (i.e: online, idle, dnd, offline)
13) `jobs` | Was updated to be: `jobs [type] [item/number]`
14) `throws` | Was updated to be like ^
15) `npm` | Updated the embed, it also supports version lookup: `npm package@version_number`
16) `stats` | The look of the embed was updated to look better and show more information.
17) `info` | Same as ^
18) `vote (-i/-info)` | It now gives you ALL of the links for the botlist sites to vote and now supports: `-i/-info` flags, you also now get tokens to use for special item(s) in the `e!shop` 
19) `avatar (@user/id)` | Now includes different formats for the user's avatar.
20) `dc/discordcolors` | Was updated to `dc [type]` (Example: `dc js`)
21) `emote` | Updated the looks of the embeds, it now includes different flags: `-url/-link`, `-steal/-create/-gimme`, `-jumbo/-big/-large` (ALSO it now supports normal emojis!, NOTE: -steal/gimme/create requires you to have Manage Emojis permission!)
22) `status [name/pageID]` | Was updated to look better and added default statuspages and you can now get the status of a custom statuspage.io ID
23) `time` | This now supports your own time that you can set with the `custom` command, you can also view other's time or one that you provide!
24) `inviteinfo`, `userinfo/whois`, `weather`, `membercount/mc`, `members`, `perms`, `roleinfo`, `rate` | Was updated to look better.
25) `ship` | Updated the embed and if there is now two users provided it picks two random members.
26) `emojis`, `roles` | Updated the embed for it and it also now supports `--ids` flag!
27) `report` | Updated the look of the embed and it also supports attachments. (NOTE: The logging of the report now requires: `Manage Webhooks` permission for the bot)
28) `boop @user` | Updated the embed and also you now have a boop counter!
29) `todo [type] [item/number]` | Updated the command completely, use it!
30) `leaderboard/lb` | Now supports `-cash` and `-bank` flags
31) `coins [add/remove]` | Now supports `all`/`half` arguments
32) `ban` | Now supports `--save` flag, to save the messages when the user gets banned. (Example: `ban @user --save [reason]`, reason is still optional) | Also supports `--silent` flag, this will make the bot not respond in the channel nor DM the user of the action!
33) `kick, softban, unban, warn` | Now supports the `--silent` flag, look above ^
34) `suggest.react1, suggest.react2` | Now supports default emojis!
35) `help` | Updated the embed, how it displays commands and now a wait time before the menu shows up. 
36) `mute, unmute` | Updated to better flow and now supports: `--silent` flag to delete the command message, `--nodm` to not DM the user when they get muted and/or when they get unmuted (the flag has to be used on the mute for the bot not to DM the user on the unmute command) AND the max time you can set for mutes is locked to **60 days** If you try to go over that it will tell you off
37) `ruser/randomuser` | Updated to `ruser [@role] (?amount)`, max amount of people returned is `30`. lowest/default is `1`






## Commands: Deleted/Replaced
1) `rep/rep+, repl` - Not really used much. 
2) `cc+, cc-, cc=, cchelp` | Replaced by: `cc [type] [?command] [?message]`, default type is: `help`
3) `docs/d.js, reverse, topinvites/invites, imdb/movie` | Never used
4) `dbl` | Replaced by: `botlist [type] [@user/id]`
5) `todo+, todo-, addtodo, removetodo` | Replaced by: `todo [type]`
6) `setrole` | Replaced by: `config [type] (@role/id)`
7) `setsuggest` | Replaced by: `config suggest.channel #channel` / `config suggest.react1 :emoji:` / `config suggest.react2 :emoji:` 
8) `reset-server, reset-left-users` | Replaced by: `reset [type] (@user/yes/no)`
9) `clearsetting` | Replaced by: `config [type] [reset/clear]`


# REQUIRED PERMISSIONS FOR THE BOT
`View Audit Logs, Manage Webhooks`: For logging, in the channel and server.

`View Channel, Send Messages, Embed Links`: In the channels for commands to work.

`Manage Server`: For welcome/leave channel logging. (read more above) AND for the `sync` command (for Integrations)

# Optional Permissions for the bot
`Manage Messages`: Required to delete user's messages 
`Manage Emojis`:  Required for the `createemoji/ce` command 
`Manage Roles`: Required for any command that requires the adding or removing of someone's roles.
