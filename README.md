# Sideline

Made by Roki Rodriguez.

A personal, all-sports Android app with a dark, broadcast-style look. Built on ESPN's public data feeds: no account,
no API key, no ads, no tracking. Everything you set up stays on your phone.

## Sports

| | Leagues |
| --- | --- |
| **US Pro** | NFL · NBA · MLB · NHL · WNBA · UFL |
| **Soccer** | Premier League · MLS · Champions League · LaLiga · Bundesliga · Serie A · Ligue 1 |
| **International soccer** | FIFA World Cup · UEFA Euro · Copa América |
| **College** | College Football · Men's College Basketball · Women's College Basketball, with AP and Coaches rankings |
| **Combat** | UFC fight cards with records, photos and results |
| **Motorsports** | Formula 1 · NASCAR Cup · IndyCar, every session with results and driver standings |
| **Golf & Tennis** | PGA Tour leaderboards · ATP and WTA draws with set scores |
| **Cricket & Rugby** | IPL and other live cricket series · Six Nations · Rugby World Cup |

## What it does

- **Home**: greeting, pinned leagues, a live-and-today rail, and a card for every team you follow with record,
  live score, next game (TV, streaming, win chance), last result, injuries and headlines.
- **Scores**: pinned leagues across the top, a day strip (week for football), live games refresh on their own.
- **Leagues**: every sport by category, each with scores, standings, rankings, teams, injuries, news and moves.
- **Team pages**: schedule and results with recent form, roster, standings, injuries, news.
- **Game pages**: score header in team colors, scoring by period, win probability, where to watch, betting line,
  live situation, scoring plays, leaders, team stats, lineups, box score, injuries, recent form and head-to-head.
- **Player pages**: bio, injury status, season and career stats, next game, news.
- **Home screen widget**: one line per followed team with the live score, next game or last result. Long-press your
  home screen, pick Widgets, then Sideline.
- **Pull down to refresh** on any list.
- **Game alerts**: optional notifications an hour before your teams play and when games end.

## Your time and place

Every time follows your phone's time zone and updates as you travel. "Today" means your today, even though ESPN files
games under US Eastern dates. Game pages also show the clock at the venue when it differs.

Set your location in Settings (use the phone's location or type a city or ZIP) and the app works out which local
channels reach you:

- National TV shows the network and the app it usually streams on, with a "Find it on your TV" link for
  over-the-air stations.
- Regional sports networks show as your local channel when you're in that team's area, or as blacked out with the
  league's out-of-market package when you're not.

TV areas are approximate. Blackouts and your provider still apply.

## Photos and logos

Header photos are real photographs from Wikimedia Commons under free licenses, credited in Settings. League and team
logos and player photos come from ESPN.

## Build the APK

This repo builds from `Sideline.zip`. The workflow unzips it, runs the parser tests, builds a signed release APK and
publishes it under Releases.

1. Delete the old `Sideline.zip` from the repo and commit.
2. **Add file → Upload files**, pick the new `Sideline.zip`, commit.
3. Open **Actions** and wait for the green check (about 5 minutes).
4. Open **Releases**, download `Sideline-<version>.apk` and install it. Every build is signed with the same key, so
   it installs over the previous version.

To work from source instead, unzip the project, push it to a repo, and the included `.github/workflows/build-apk.yml`
builds on every push.

## Notes

- ESPN's feeds are public but unofficial. If a feed changes, that screen may come up empty until the parser is
  updated. Every screen has a retry, and one broken item never takes down a list.
- Sideline collects zero personal data and stores all preferences locally on this device.
- For personal use. Team names and logos belong to their leagues and teams.

## Project layout

```
app/src/main/java/com/roki/sideline/
  data/   Models.kt   league catalog and models       Espn.kt     feeds, cache, local-day logic
          Parse.kt    JSON to models (all sports)      Local.kt    favorites, pins, streaming map, prediction, formatting
          Tv.kt       where to watch, by location      Where.kt    location        Places.kt  team markets, venue clocks
          Art.kt      photos and league logos
  work/   Alerts.kt   game-time and final-score notifications
          SidelineWidget.kt   home screen widget
  ui/     Theme, Kit (design system), HomeScreen, Browse (Scores, Leagues, Settings), LeagueScreen, EventViews,
          Games (game cards and game page), TeamScreen (team and player pages)
app/src/test/   parser and time-zone tests on ESPN-shaped samples
```
