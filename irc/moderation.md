# Cheatsheet for IRC OPs
- [General Notes](#general-notes)
- [Channel and Usermodes](#channel-and-usermodes)
  * [Possible Channelmodes in Freenode's IRC Network](#possible-channelmodes-in-freenodes-irc-network)
  * [Possible Usermodes in Freenode's IRC Network](#possible-usermodes-in-freenodes-irc-network)
- [Channel Creation and Registration](#channel-creation-and-registration)
- [Op and DeOp](#op-and-deop)
- [Topics](#topics)
- [Masks](#masks)
- [Kicks and Bans](#kicks-and-bans)
- [Muting Users](#muting-users)
- [Channelmodes](#channelmodes)
  * [Moderated Mode](#moderated-mode)
  * [Registered Only Mode](#registered-only-mode)
- [Managing Users](#managing-users)

<small><i><a href='http://ecotrust-canada.github.io/markdown-toc/'>Table of contents generated with markdown-toc</a></i></small>

### General Notes

Commands are displayed using the following syntax: `/some_command`

User specified parameters are within diamond brackets: `<user_defined_parameter>`

Optional parameters are within square brackets: `[<optional_user_defined_parameter>]` 

If the user has to choose between multiple possibilities it is indicated using round brackets and a pipe symbol to separate several possible values: `(<possibility_one>|<or_possibility_two>)`

## Channel and Usermodes

Many things on IRC networks are handled using so called modes. These can be either applied to users or channels using the following syntax:

`/mode (<nickname>|<channelname> (+|-)<mode> [<additional_parameters>]`

whereby `+` activates, and `-` deactivates the given mode.

To list current modes this command can be used:

`/mode (<nickname>|<channelname>)`

### Possible Channelmodes in Freenode's IRC Network
[source](https://freenode.net/kb/answer/channelmodes)

| Mode(name)        | Description                                                       |
|-------------------|-------------------------------------------------------------------|
|b (channel ban)    | Prevent users from joining or speaking. Sending `/mode #channel +b` alone will return the current ban list. While on the channel, banned users will be unable to send to the channel or change nick. The most common form for a ban is `+b nick!user@host`. The wildcards `*` and `?` are allowed, matching zero-or-more and exactly-one characters, respectively. Bans set on IP addresses will apply even if the affected user joins with a resolved or cloaked hostname. CIDR notation is supported in bans. The second form can be used for bans based on user data. You can append `$#channel` to any ban to redirect banned users to another channel.|
| c (colour filter) | Strip colour and formatting codes from channel messages. |
| C (block CTCPs)   | Blocks CTCP commands (other than `/me` actions). |
| e (ban exemption) | Takes one parameter, just like ban (above). Wildcards and extbans can be used, like ban. Ban exemption matches override `+b` and `+q` bans for all clients it matches, allowing the exempted user to join/speak as if they were not banned or quieted. This can be useful if it is necessary to ban an entire ISP due to persistent abuse, but some users from that ISP should still be allowed in. For example: `/mode #channel +bee *!*@*.example.com *!*someuser@host3.example.com $a:JohnDoe` would block all users from `example.com`, while still allowing someuser from `host3` and `JohnDoe` to join. |
| f (forward) | Takes a channel name as a parameter. Users who cannot join the channel (because of `+i`, `+j`, `+r`, see below) are instead sent to the given channel. Clients are notified when the forward takes effect. An operator can set `mode +f #channel2` only if they are an op in `#channel2` or if `#channel2` has `mode +F` set (see below). Usually you want to set forwards with MLOCK, because the channel will become empty over time and the channel modes are lost. You might also want to set `GUARD` to prevent the channel from becoming empty. An operator can use MLOCK with `+f` only if they have access flag `+s` in both channels, or if the channel to be forwarded to is `+F` and they have `+s` in the original channel. |
| F (enable forwarding) | Allow operators in other channels to forward clients to this channel, without requiring ops in the target channel. |
| g (free invite) | Anybody in the channel may invite others (using the `/invite` command) to the channel.|
| i (invite only) | Users are unable to join invite-only channels unless they are invited or match a `+I` entry. |
| I (invite exemption) | Takes a ban parameter. Extbans are supported and common, e.g. for setting an exemption for a specific registered user. Matching clients do not need to be invited to join the channel when it is invite-only (`+i`). Unlike the `/invite` command, this does not override `+j`, `+l` and `+r`. Only channel operators can see `+I` changes or see the list with `/mode #channel +I`. |
|j (join throttle) | This mode takes one parameter of the form n:t, where n and t are positive integers. Only n users may join in each period of t seconds, so with e.g. 3:10 only 3 users could join within 10 seconds. Invited users can join regardless of `+j`, but are counted as normal. You can use this mode to prevent bot attacks. Observe the average join rate of your channel and pick a good value for `+j`. This mode could be combined with `+f` to forward throttled users to an overflow channel. |
| k (password) | To enter the channel, you must specify the password on your `/join` command. Keep in mind that modes locked with ChanServ's MLOCK command can be seen by anyone recreating the channel; this includes keys. Also keep in mind that users being on the channel when `+k` is set will see the key as well. |
| l (join limit) | Takes a positive integer parameter. Limits the number of users who can be in the channel at the same time. |
| m (moderated) | Only opped and voiced users can send to the channel. This mode does not prevent users from changing nicks. |
| n (prevent external send) | Users outside the channel may not send messages to it. Keep in mind that bans and quiets will not apply to external users. |
| p (private) | The KNOCK command cannot be used on the channel, and users will not be shown the channel in whois output unless they share the channel with the requestor. The channel will still appear in channel lists and WHO output (set channel `mode +s` if this is not desired).|
| q (quiet) | Works like `+b` (ban user), but allows matching users to join the channel.|
| Q (block forwarded users) | Users cannot be forwarded (see `+f` above) to a channel with `+Q`. |
| r (block unidentified) | Prevents users who are not identified to services from joining the channel. |
| s (secret) | This channel will not appear on channel lists or WHO or WHOIS output unless you are on it. |
| S (SSL-only) | Only users connected via SSL may join the channel while this mode is set. Users already in the channel are not affected. Keep in mind that this also blocks all webchat users, as they are not marked as connected via SSL. |
| t (ops topic) | Only channel operators may set the channel topic. |
| z (reduced moderation) |  The effects of `+b`, `+q`, and `+m` are relaxed. For each message, if that message would normally be blocked by one of these modes, it is instead sent to channel operators (`+o`). |

### Possible Usermodes in Freenode's IRC Network
[source](https://freenode.net/kb/answer/usermodes)

| Mode (name)    |  Description                                      |
|----------------|---------------------------------------------------|
| g (caller-id)  | Ignores private messages from unknown users, instead informing you someone is attempting to message you. You can choose to receive messages with the `/accept` command. Messaging a user automatically accepts them. |
| i (invisible)  | Hides you from global WHO/WHOIS by normal users, and shows only shared channels in `/WHOIS` output. |
| Q (disable forwarding) | Prevents channel forwards from affecting you. If a channel's modes prevent you from joining, you will receive the relevant error message regardless of any forwards. |
| R (block unidentified) | Ignores private messages from users who are not identified with services. |
| w (see wallops) | Subscribes you to /wallops messages from freenode staff. Used infrequently to highlight interesting announcements from the FOSS community. You will receive important network announcements irrespective of this setting. |
| Z (connected securely) | Set automatically by the network when you connect via SSL/TLS. |

On Freenode `+Z`and is set automatically if you connect using SSL/TLS. `+i` is set per default and can be unset by the user.

## Channel Creation and Registration

Choosing a channel name

On the Freenode-Network normal channel should have a name like `##<channelname>` only registered primary groups should use `#<channelname>` in all following snippets `<channelname>` includes `#` or `##`!

`/join <channelname>` 

Check if a channel is already registered

`/msg Chanserv info <channelname>` 

Register a channel

`/msg Chanserv register <channelname>` 

## Op and DeOp

Gain/give OP status

`/msg Chanserv op <channelname> [<nickname>]`

Drop/remove Op status

`/msg Chanserv deop <channelname> [<nickname>]` 

The nickname is optional each. If it is omitted, you will (de)op yourself.

---

**For all of the following commands you need to have the op status!**

## Topics

Reading the topic

`/topic <channelname>`

Setting a topic

`/topic <channelname> <new topic>` 

## Channel Entry Messages

To set a new channel entry message simply use

`/msg ChanServ SET <channelname> ENTRYMSG [<message>]`

If you don't want to have a channel message just leave the message blank.

## Masks

`<nickname>!<ident>@<hostname>.<domainname>`

| Segment      | Description                                                                    |
| ------------ | ------------------------------------------------------------------------------ |
| `nickname`   | The users nickname as normaly shown in the userlist                            |
| `username`   | User name chosen by the client. Typically the username on the clients computer |
| `hostname`   | The users host, used to connect to the irc server                              |
| `domainname` | Domain for the users hostname                                                  |

The `hostname` and `domainname` sometimes is substituted by a *cloak*. This is done to hide the users origin. **This is no real security feature! It does not provide any anonymity!** On the freenode servers this typically looks like `unaffiliated/<nickname>`.

Within these masks it is possible to use wildcards `*` as well as a limited set of regex. Here some examples (✓is included in the mask; 𐄂 is not included):

**`*!*@<hostname><domainname>` ➞ any nick and any user comming from `<hostname><domainname`**

 `*!*@unaffiliated/test`:

- `test!linux@unaffiliated/test` ✓

- `test!linux@test/unaffiliated` 𐄂

- `nottest!wintest@unaffiliated/test` ✓

**`<nickname>!*@*` ➞ `<nickname>` which uses any username from any origin (hostname/domainname)**

`spammer!*@*`:

- `spammer!random@asian-vpn-18.com` ✓

- `anotherspammer!random@asian-vpn-18.com` 𐄂

- `spammer!kiwi@kiwiirc/98.11.20.12` ✓

In case of nick-only masks the rest of the mask can be omitted, so it's also valid to simply use:
- `spammer`
- `someOnetoKickOrBan` 

It is also possible to use the wildcards only for a part of the usermasks segments. E.g.:

**`<partial-nick>*!*@*` ➞ any `<nickname>` starting with `<partial-nick>` with any `<ident>` from any `<hostname><domainname>`** 

`spam*!*@*`:

- `spamalot!kiwi@kiwiirc/21.123.234.12` ✓

- `alotspam!kiwi@kiwiirc/21.123.234.12` 𐄂

- `spam!nop@unaffilitated/spamalot` ✓

## Kicks and Bans
Kick an user. Giving a `<reason>` is optional

`/kick <channelname> <nickname> [<reason>]`

Basic ban

`/mode <channelname> +b <nickname>!<ident>@<hostname><domainname>`

Basic unban

`/mode <channelname> -b <nickname>!<ident>@<hostname><domainname>`

Instead of `<nickname>!<ident>@<hostname><domainname>` it is also possible to use *Masks* like shown before. In such case all users who are catched by the Mask are banned.

## Muting Users

Basic mute

`/mode <channelname> +q <nickname>!<ident>@<hostname><domainname>`

Basic unmute

`/mode <channelname> -q <nickname>!<ident>@<hostname><domainname>`


## Channelmodes

An overview of all possible channelmodes at the Freenode network can be found [above](#possible-channelmodes-in-freenodes-irc-network).

### Moderated Mode

This mode can be extremely useful if there are some spammers anoying a whole channel. If this mode is active, users need to be voiced to be able to read message of other users. Only Ops are able to read all messages (even of unvoiced users). To activate the moderated mode use:

`/mode <channelname> +m`

and to deactivate use

`/mode <channel> -m`

To voice users you can use the `mode` command as well:

`/mode <channelname> +v <nickname>`

to give multiple users at once voice you can add a `v` per user and simply append the nickname to the command. For example if you want to voice two users at once:

`/mode <channelname> +vv <nickname> <another_nickname>`

### Registered Only Mode


## Managing Users




