# Cheatsheet for IRC OPs

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

`/msg Chanserv op <channelname> <nickname>`

Drop/remove Op status

`/msg Chanserv deop <channelname> <nickname>` 

---

**For all of the following commands you need to have the op status!**

## Topics

Reading the topic

`/topic <channelname>`

Setting a topic

`/topic <channelname> <new topic>` 

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

## Managing Ops




