# EQSidekick

Mazilla AB · October 2026 · [Download the latest release](https://github.com/mmarpik/EQSidekick-releases/releases/latest)

## Abstract

EQSidekick turns the logs every raider already writes into one shared record of the raid, with no extra work in game.

- **The whole fight, not one client's view.** Every raider's log is merged into one night, each event counted once. A single log misses hits: on one boss, the main's log alone saw 95.5% of the fight.
- **Raids that organise themselves in Discord.** Signups work the way the guild signs up today, and the planner turns them into groups in one click: a healer in every group and every signup line kept together, on all 15 real raid nights we replayed.
- **A raid history that stays.** Attendance, groups, loot and DKP live on the guild's raid server, for officers on any PC and members on the web and their phone.

## At a glance

Each raider's meter reads their own logs and uploads them; the raid server merges them into one night and holds raids, groups, signups and loot; Discord and the phone app read and write the same raids.

## Compared with EQLogParser

EQLogParser is the best single-log parser for EverQuest, and EQSidekick does not try to beat it at that. EQSidekick starts where one log stops: it combines every raider's log into one raid, keeps what it learns on a shared server, and brings the results to Discord.

|  | EQLogParser | EQSidekick |
| --- | --- | --- |
| Logs read | One log at a time, on one PC | Every active log on the PC at once (a main and its boxes), and every raider's log merged on the raid server |
| What one fight is measured from | What your client happened to show you | Everything any raider's client showed, counted once |
| Where knowledge lives | On your PC | On the guild's raid server: raids, attendance, groups, signups, loot, rosters |
| Triggers | GINA-compatible, text-to-speech on your PC | GINA-compatible, a voice per character, Azure's neural voices; callouts in the raid's Discord voice channel being tested |
| Discord | Share a parse as text | Raid signups and raid channels; fight posts and voice callouts being tested |
| Raid organisation | Not covered | Signups, group planning, loot and DKP, a phone app |
| Damage, healing and tanking detail | Deep: by ability, spell counts, trends across fights | Abilities, healing and tanking from the whole raid's merged logs, burns by group, after-fight analysis |

### One raid, many logs

EverQuest shows each client only part of a raid fight, so any single log misses hits. On the Oct 20 raid, two characters on one PC each saw events the other missed: about 9,000 only in the main's log, about 23,700 only in the box's. On one boss, the main's log alone saw 95.5% of the fight.

EQSidekick merges logs at two levels:

- **On the PC:** a main and its box are read together as one meter while they are in the same raid. A box elsewhere is left out, with the reason shown, and can open in its own window.
- **On the raid server:** every raider's upload is merged into one night. The same event seen by several players counts once; what only one saw is kept. Merged totals match the server's within 0.01% per fight.

### Knowledge that stays

A parser forgets when you close it. The raid server keeps every raid night: who signed up, who came, the groups as planned and as formed in game, the raid lists, loot and the guild roster. Officers see it from any PC, and members on the guild's web pages and phone app. Past raids can be backfilled from old logs and raid lists: September and October 2026 were loaded this way. The raid server is either the hosted one at raid.mazilla.se or the guild's own, from a download with a setup guide.

### Triggers in your voice, and in Discord

Triggers import from GINA packages. Each character has its own trigger setup and its own voice, so a main and its box can be told apart by ear; an alert both see is said once. Alerts can be said in Azure's neural voices. Being tested: a Discord voice bot that speaks the raid's callouts in the voice channel, so everyone hears the same warning at the same moment, whether or not they run triggers themselves.

### Automatic Discord posts

Being tested: after each fight, the meter can post the result to the guild's Discord, as text or as images: a summary card, the full table and a damage graph. A text post looks like this (names made up):

```text
**Rufus Invictus** · 6:57 · 252M damage @ 36.3M · Oct 20 20:02
    Player            Damage      DPS   Time
 1. Joku              21.4M     3.08M   412s
 2. Brightblade +Pets 19.9M     2.86M   405s
 3. Emberwisp         18.7M     2.69M   398s
```

## Discord signups

EQSidekick's signup bot works the way guilds already sign up, so a guild can switch to it without anyone noticing, and only then start using what it adds.

**Signing up**

- `!join Thornwick, Mirabel, Oskarr` in the guild's sign-up channel, exactly as today. One line is one group for the night: the characters on it come together.
- `!maybe`, `!late`, `!out` and `!leave` change an answer. A note after the names ("may be a little late") is kept, and an unsure note makes it a Maybe.
- `/signup` does the same with autocomplete of the guild's characters. Anyone may sign up someone else, and the signer is recorded.
- A typo gets a short reply: "Don't know Thornwik: did you mean Thornwick?" Everything else gets a ✅.

**Raids without extra work**

- The raid leader's own "Sign-ups are open for Tuesday, Oct 20!" post creates the raid. So does `/raid create`, which posts that opener in the guild's own wording and ping.
- A "Raid cancelled" post or `/raid cancel` cancels it, and the signups are kept.
- Optionally, a Discord channel and scheduled event per raid; or everything stays in one sign-up channel.

**Switching over quietly**

1. **Listen:** the bot runs beside the old bot, reads every line and records it, and never says a word in Discord. It only needs to read the channel.
2. **Compare:** officers see what the bot recorded, and what it would have answered, on the raid's page.
3. **On:** turn the old bot off and EQSidekick on. With the "Added <3" reply style, the channel looks the same as before.

Signups land in the raid planner, on the guild's web pages and in the phone app, where members can also answer from their phone.

## Raid groups

The raid planner turns tonight's signups into groups in one click, the way an experienced raid leader builds them, and then checks the raid as formed in game against the plan.

**What it does**

- **Auto-assign** fills group templates (tank, melee, caster) from a preset: a healer in every group, bards spread where they help most, a box always with its main.
- **Group-mates stay together:** each signup line is one group, and players who usually group together are kept together, learned from the last 10 raids.
- **Officers' standing rules** ("never with their boxes", "always with") apply to every raid until removed.
- **Drag and drop** for the final touches, with the reason each player was placed shown on hover.
- **In game vs plan:** once the raid is formed and someone writes a raid list (`/outputfile raid`), the planner pairs each planned group with the in-game group that shares the most members, whatever its number, and lists the moves that make the raid match the plan, in an order that works. The raid list can come from any officer's meter.

**How close it gets to a human raid leader**

We replayed 15 real raid nights (Sep 1 to Oct 22, 2026; 649 characters, 114 groups) through the planner and compared its groups with the ones the raid leader actually posted.

| Measure | Planner | Raid leader |
| --- | --- | --- |
| Groups with a healer | 114 of 114 | 114 of 114 |
| Signup-line pairs kept together | 387 of 387 | 366 of 387 |
| Caster groups with a bard | 60% | 58% |
| Groups with two bards | 0 | 0 |

The hard rules match on every night. The raid leader still makes the final calls: the planner gives a starting point that follows the guild's own rules, and two rules found by this comparison are already in it: lines join their usual group-mates, and the second melee group comes later.

## Loot

EQSidekick reads every item that drops straight from the log, so the loot officer keeps track of the raid's loot without writing anything down, and DKP follows by itself.

- **Every drop, in one list:** time, item, who took it, how (looted, rolled, auctioned), from which corpse and in which fight. Rolls are listed highest first. Items left on a corpse are shown, and raid loot left behind is marked red in case it was a mistake. Trash loot can be hidden.
- **Item cards:** hovering an item shows its stats from the item database.
- **Auctions in raid chat:** put an item up with one click, and the helper reads bids from raid chat or tells. It supports sealed bids by /tell, second-price wins and a minimum raise, and copies the opening, status and result lines to paste in /rs.
- **OpenDKP:** for guilds on OpenDKP, the meter sends attendance ticks from raid lists, and each auction's winner and price as an item.
- **On the guild's web pages:** loot, DKP, auctions and an item list for every raid on the server.

Loot can be shown for one night, one raid or a range of nights, and grouped by item: each item's count, expanding to who looted it, when and from which corpse.

## After the fight

After each fight, EQSidekick answers "what went wrong, and what should I do differently?" from the facts in the logs, for the whole raid or for one player, with optional coaching from Claude.

- **A facts sheet per fight:** deaths with the last seconds before each, damage on each mob (pets shown apart), burns used, casts per minute and the casts beside a player's own. It covers the whole raid or one player, from your log or from the raid's merged night on the server.
- **Coaching on request:** one click sends the sheet, and only the sheet, to Claude, which answers with strengths, things to improve and a question to think about. Every point cites the facts it rests on, and a point that cites nothing on the sheet is dropped. Nothing leaves the PC until the button is pressed.
- **Analysis for officers:** statistics per player and per class (damage taken and avoided, crippling blows, twincasts, fizzles, interrupts, mez breaks, rez casts, cleanses), abilities per player, and a filterable list of mobs.
- **Playback:** the fight replayed second by second, with each player's activity in swimlanes.
