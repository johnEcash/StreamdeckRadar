# Flight Radar for Stream Deck

See the air traffic above your location, live on your Elgato Stream Deck.
Flight Radar shows the nearest aircraft, a radar view, altitude, speed, country of registration (with flag), low-pass warnings and military aircraft. On a **Stream Deck+** you can zoom, browse aircraft and filter with the dials.

![Flight Radar on a Stream Deck+](docs/mockup.png)

---

## Contents

- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Setup](#setup)
  - [1. Create a free OpenSky account](#1-create-a-free-opensky-account)
  - [2. Create an API client](#2-create-an-api-client)
  - [3. Find your coordinates](#3-find-your-coordinates)
  - [4. Add the actions and enter your settings](#4-add-the-actions-and-enter-your-settings)
- [Actions](#actions)
  - [Keys](#keys)
  - [Dials (Stream Deck+)](#dials-stream-deck)
- [Settings](#settings)
- [Credits and refresh rate](#credits-and-refresh-rate)
- [Military aircraft](#military-aircraft)
- [Language](#language)
- [Troubleshooting](#troubleshooting)
- [Privacy](#privacy)
- [Data sources and attribution](#data-sources-and-attribution)
- [Disclaimer](#disclaimer)

---

## Features

- **Nearest aircraft** with callsign, distance, direction and an arrow showing where it is heading
- **Radar view** with you in the centre and every aircraft as a dot, north up
- **Altitude** with climbing / descending indicator, and **speed** with track
- **Country of registration** with the country's flag, for every country in the world
- **Low-pass warning**: the key turns orange when an aircraft flies below an altitude you choose
- **Military aircraft**: shown first and highlighted in red, with a dedicated key
- **Stream Deck+ dials**: change the radius, browse through aircraft, filter by altitude and choose the refresh interval, all shown on the touch strip
- **English and Dutch**, switchable in the settings
- **Careful with your data allowance**: one shared request for all keys, and no requests at all when no Flight Radar key is visible

## Requirements

| | |
|---|---|
| **Stream Deck app** | version 6.5 or newer |
| **Operating system** | Windows 10 or newer, or macOS 12 or newer |
| **Stream Deck hardware** | any Stream Deck for the keys; a **Stream Deck+** for the dial actions |
| **OpenSky Network account** | free; needed to receive flight data (see [Setup](#setup)) |
| **Internet connection** | yes |

## Installation

1. Download the file **`com.johnecash.flightradar.streamDeckPlugin`** from the [Releases](../../releases) page of this repository.
2. Double-click the downloaded file.
3. The Stream Deck app opens and asks whether you want to install **Flight Radar**. Click **Install**.
4. In the list of actions on the right side of the Stream Deck app you will now find a category called **Flight Radar**.

To update to a newer version later, simply download and double-click the new file. Your settings are kept.

## Setup

Flight Radar gets its data from the [OpenSky Network](https://opensky-network.org), a non-profit community network of aircraft receivers. You need a free account and an "API client" (a personal key) so the plugin can request data on your behalf.

### 1. Create a free OpenSky account

1. Go to [opensky-network.org](https://opensky-network.org).
2. Click **Register** (top right) and create an account.
3. Confirm your e-mail address using the link OpenSky sends you, then log in.

### 2. Create an API client

1. While logged in, open your **Account** page on the OpenSky website (via your user name at the top right).
2. Find the section for **API clients** and create a new client. Give it a name you will recognise, for example `stream-deck`.
3. Download the credentials file. It is called **`credentials.json`** and contains two values: a `client_id` and a `client_secret`.
4. Open `credentials.json` with a text editor:
   - **Windows:** right-click the file → **Open with** → **Notepad**
   - **macOS:** right-click the file → **Open With** → **TextEdit**
5. Keep this window open; you will copy the two values into the plugin in step 4.

> Treat `client_secret` like a password. Don't share it or post it in screenshots.

### 3. Find your coordinates

The plugin needs the latitude and longitude of the place you want to watch (usually your home).

1. Open [Google Maps](https://maps.google.com) on your computer.
2. Find your location and **right-click** exactly on it.
3. The first line of the menu shows two numbers, for example `51.21234, 4.40567`. Click them to copy.
4. The first number is your **latitude**, the second your **longitude**.

Two or three decimals are more than enough.

### 4. Add the actions and enter your settings

1. In the Stream Deck app, open the **Flight Radar** category in the list on the right.
2. Drag an action, for example **Nearest**, onto a key.
3. Click that key in the Stream Deck app. The settings panel appears at the bottom.
4. Fill in:
   - **Client ID**: the value of `client_id` from `credentials.json` (without the quotation marks)
   - **Client secret**: the value of `client_secret` (without the quotation marks)
   - **Latitude** and **Longitude**: the numbers from step 3, with a **dot** as decimal separator
5. After a few seconds the key shows the nearest aircraft.

The settings are **shared by all Flight Radar actions**, so you only need to enter them once. Add as many other actions as you like; they start working immediately.

## Actions

### Keys

| Action | What it shows | Press |
|---|---|---|
| **Nearest** | Callsign, distance and direction of the first aircraft in the list (a military aircraft if there is one and "Military always first" is on, otherwise the nearest). The arrow shows the aircraft's direction of flight. When you select another aircraft with the Aircraft dial, the label changes to e.g. `AIRCRAFT 3/12`. | Refresh now |
| **Nearby** | Number of aircraft within your radius | Refresh now |
| **Radar** | Radar view: you are the blue dot in the centre, north is up. Orange dots are aircraft, red dots military aircraft. The selected aircraft has a ring. | Refresh now |
| **Altitude** | Altitude of the selected aircraft, with a blue arrow when climbing, an orange arrow when descending, or a line when level | Refresh now |
| **Speed** | Ground speed in km/h and track (direction of flight in degrees) | Refresh now |
| **Country** | Country of registration of the selected aircraft, with flag | Refresh now |
| **Low Pass** | Normally dark. Turns **orange** when an aircraft flies below the altitude set in *Low pass below*, showing its altitude, callsign and position | Refresh now |
| **Military** | Normally dark with "None". Turns **red** when there are military aircraft within your radius, showing the nearest one and the total number in a white circle | Select that military aircraft on all keys |
| **Update** | Time since the last successful refresh and your remaining OpenSky credits for today | Refresh now |

*"Selected aircraft"* means the first aircraft in the list, unless you picked another one with the **Aircraft** dial or the **Military** key.

A **small orange dot** in the top-right corner of a key means the last refresh failed and you are looking at the previous data. See [Troubleshooting](#troubleshooting).

### Dials (Stream Deck+)

These actions can only be placed on the dials of a Stream Deck+. Each one has its own section on the touch strip.

| Dial | Turn | Push the dial or tap the touch strip |
|---|---|---|
| **Radius** | Radius larger or smaller, in steps of 5 km (5 to 150 km) | Back to 50 km |
| **Aircraft** | Browse through the aircraft, from first to last. All keys follow the selected aircraft. | Back to the first aircraft |
| **Min. Altitude** | Hide aircraft below this altitude, in steps of 250 m | Filter off |
| **Refresh** | Choose the refresh interval: 30 s, 1, 2 or 5 minutes. The touch strip shows the estimated credits per day. | Refresh now |

Changes made with the dials are saved and also appear in the settings panel.

## Settings

Click any Flight Radar key or dial in the Stream Deck app to open the settings.

| Setting | Description | Default |
|---|---|---|
| **Taal / Language** | Language of the keys, touch strip and settings panel: Nederlands or English | Nederlands |
| **Client ID** / **Client secret** | Your OpenSky API client (see [Setup](#2-create-an-api-client)) | — |
| **Latitude** / **Longitude** | Your location, with a dot as decimal separator | — |
| **Radius (km)** | How far around you to look, 5 to 150 km | 50 |
| **Min. altitude (m)** | Hide aircraft below this altitude; `0` shows everything | 0 |
| **Low pass below (m)** | Altitude under which the **Low Pass** key lights up | 1000 |
| **Military always first** | Put military aircraft at the top of the list | on |
| **Callsign codes** | Extra callsign prefixes treated as military, separated by commas. Leave empty for the default list: `BAF, NAF, GAF, RRR, CTM, FAF, RCH, NATO, MMF, IAM, AME, PLF` | default list |
| **Interval** | How often to refresh: 30 s, 1, 2 or 5 minutes | 30 s |

Note: the altitude filter also applies to the **Low Pass** key. If *Min. altitude* is higher than *Low pass below*, the Low Pass key can never light up.

## Credits and refresh rate

OpenSky gives every free account a daily allowance of **API credits**. With a free account this is **4,000 credits per day**.

- Every refresh costs **1 credit** (for any radius up to 150 km).
- All Flight Radar keys and dials share **one** request, so having many keys does not cost more.
- When no Flight Radar key or dial is visible (for example because you switched to another page or profile), the plugin **stops requesting data** and uses no credits.
- Turning the Radius dial waits until you stop turning before requesting new data, so one turn of the dial costs only one credit.

| Interval | Credits per day (if visible all day) |
|---|---|
| 30 s | about 2,880 |
| 1 min | about 1,440 |
| 2 min | about 720 |
| 5 min | about 288 |

The **Update** key shows how many credits you have left today.

## Military aircraft

OpenSky itself does not mark aircraft as military. Flight Radar recognises them in two ways:

1. A list of aircraft tagged as military by the community service [adsb.lol](https://adsb.lol), matched by transponder address. This list is fetched at most once a minute and **does not use any OpenSky credits**.
2. Callsign prefixes of known military operators (see **Callsign codes** in the [Settings](#settings)).

Military aircraft are shown in **red** on the Nearest, Altitude, Speed, Country and Radar keys and on the Aircraft dial, and the **Military** key turns red.

> Many military flights switch off their ADS-B transmitter. Those aircraft are not visible in OpenSky or adsb.lol, so Flight Radar cannot show them either.

## Language

Choose **Taal / Language** at the top of the settings panel. The keys, touch strip and settings panel switch immediately between Dutch and English. Numbers follow the language as well (`10.670 m` / `10,670 m`).

The names of the actions in the Stream Deck action list are always in English.

## Troubleshooting

| What you see | What it means | What to do |
|---|---|---|
| **Settings missing** | Client ID, client secret, latitude or longitude is empty or invalid | Open the settings and fill in all four fields. Use a **dot** in the coordinates (`51.21`, not `51,21`). |
| **Login failed** | OpenSky does not accept your client ID or secret | Copy both values again from `credentials.json`, without quotation marks or spaces. If that doesn't help, create a new API client on the OpenSky website. |
| **Out of credits** | You used today's OpenSky credits | Wait until the next day, and choose a longer interval with the Refresh dial or in the settings. |
| **API error 5xx** or **Network error** | OpenSky is temporarily unavailable, or there is no internet connection | Usually solves itself; the plugin keeps trying at the chosen interval. |
| **Small orange dot** on a key | The last refresh failed; you see the previous data | See the rows above; the **Update** key shows the error. |
| **No aircraft** | No aircraft within your radius (or all hidden by *Min. altitude*) | Increase the radius, set *Min. altitude* to 0, or try again at a busier time of day. |
| **Grey flag with "?"** on the Country key | The country name is not yet known to the plugin | Please [open an issue](../../issues) with the country name shown on the key. |
| Keys stay on **Loading…** | The plugin has not received data yet | Check your internet connection and settings. Pressing a key forces a refresh. |

If a problem persists, restart the Stream Deck app: right-click the Stream Deck icon in the system tray (Windows) or menu bar (macOS) and choose **Quit**, then start the app again.

## Privacy

- Your **client ID and secret** and all other settings are stored locally by the Stream Deck app on your computer. They are not part of the plugin file and are never sent anywhere except to OpenSky to log in.
- To request flight data, the plugin sends OpenSky a rectangular area around your location (the size of your radius). Your exact coordinates are not sent.
- The military list is downloaded from adsb.lol as a whole; nothing about you or your location is sent to adsb.lol.
- The plugin does not collect statistics or send data anywhere else.

## Data sources and attribution

- Flight data: **[The OpenSky Network](https://opensky-network.org)**. Free use is intended for research and non-commercial purposes; see the OpenSky terms of use.
- Military aircraft list: **[adsb.lol](https://adsb.lol)**, available under the [Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/).
- Flags are simplified drawings made for this plugin; complex coats of arms are shown in simplified form.

## Disclaimer

Flight Radar is a hobby project for fun and curiosity. The data can be delayed, incomplete or incorrect. **Do not use it for navigation, safety or any operational purpose.**

This project is not affiliated with or endorsed by Elgato, Corsair, the OpenSky Network or adsb.lol. Stream Deck is a trademark of Corsair Memory, Inc.
