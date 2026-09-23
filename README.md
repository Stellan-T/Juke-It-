# Juke it! Spotify edition: setup guide

This version plays songs from your own Spotify playlists, without anyone seeing what's playing. You set it up once, which takes about 15 minutes.

**You need:**

- A Spotify Premium account for the host.
- A free Netlify account, or any other place that can host a website.

## 1. Put the game online

Spotify only talks to games that live at a real web address, so the game can't run as a file on your computer.

1. Go to **app.netlify.com/drop** and create a free account.
2. Drag the whole `jukeit-spotify` folder onto the page.
3. Netlify gives you an address like `https://cheerful-jukebox-123.netlify.app`. Open it, and the game shows its connection screen.

GitHub Pages works too if you prefer it. Any host that serves the site over `https://` is fine.

## 2. Register the game with Spotify

1. Go to **developer.spotify.com/dashboard** and log in with the host's Premium account. Accept the terms if asked.
2. Click **Create app** and fill it in:
   - **App name:** Juke it!
   - **App description:** Personal music party game
   - **Redirect URI:** paste the address the game shows under "Your app's address" and click **Add**. It must match exactly, including the `/` at the end.
   - **Which API/SDKs are you planning to use:** tick **Web API**.
3. Save the app. On the app's page, open **Settings** and copy the **Client ID**, a 32-character code.
4. Open **User Management**. Add the name and email of every Spotify account that will host games, up to 5. Each of those accounts needs Premium.

## 3. Connect

1. Open the game, paste the Client ID and tap **Log in with Spotify**.
2. Approve the permissions. You're sent back to the game, and it stays logged in on that phone.

If you don't want to type the Client ID on every new phone, open `index.html` in a text editor. Put the ID between the quotes in `const DEFAULT_CLIENT_ID = "";` and upload the folder again.

## Before each game night

- **Turn off Autoplay in Spotify:** go to Settings, then Playback, then Autoplay. Otherwise Spotify keeps playing other songs after the mystery song ends.
- **Wake up the phone's Spotify:** open the Spotify app, play any song for a second and pause it. That makes the phone show up as a device the game can play on. You can pick the device in the game's settings (the gear icon).
- **iPhone:** the first time you draw a song, allow access to "Motion & Orientation". That's how the game knows the phone is face-down.

## How a turn works

1. The player taps **Draw a song** and puts the phone face-down on the table.
2. The song starts as soon as the screen is down. If the phone can't sense being flipped, use the 3-second countdown and put it down before zero.
3. Pick the phone up and place the song on your timeline. The game screen never shows the title until the reveal.

One small leak: while music plays, some phones show a tiny album cover in the notification area. On iPhone that's the Dynamic Island. If your group is competitive, place cards without looking at the top of the screen.

## Playlists

The game merges every playlist you pick into one shuffled deck, with duplicates removed.

Spotify only lets this game read:

- **Playlists the host made.**
- **Playlists the host was invited to as a collaborator.**

To use a friend's playlist, they open it in Spotify and choose **Invite collaborators**, and the host accepts. The easier option is to make one collaborative "Game night" playlist that everyone adds songs to.

## Release years

Spotify often lists a remaster or compilation year. For example, a 1976 song can show up as 2014. So the game checks every song against MusicBrainz, a free music database, and keeps the earliest real release year.

It looks up about one song per second in the background while you play. If a year still looks wrong at the reveal, tap **Year wrong? Fix it**. The game re-checks that turn with the corrected year and remembers the correction for future games.

## Troubleshooting

- **"INVALID_CLIENT: Invalid redirect URI":** the address in the Spotify dashboard doesn't match the game's address exactly. Copy it from the game's connection screen again.
- **Login works but then errors with 403:** that account isn't listed under User Management, or the app owner's Premium has lapsed.
- **"Spotify can't find the phone to play on":** open the Spotify app, play and pause a song, then pick the device again in the game's settings.
- **The phone doesn't react to being flipped:**
  - On iPhone, the motion permission was denied. Clear the website data in Safari's settings, then reload the game.
  - Otherwise, use the countdown button.
- **The phone locked mid-game:** the game asks the screen to stay on, but some battery-saver modes override that. Turn battery saver off while playing.

## A note on Spotify's rules

Spotify's developer policy doesn't allow games built on its API. This is a personal project for up to 5 accounts, but Spotify can switch off the app's access at any time. If that happens, the game stops being able to read playlists and play songs.
