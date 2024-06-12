### !! You must first install [MP4Box](https://gpac.io/downloads/gpac-nightly-builds/), and ensure [MP4Box](https://gpac.io/downloads/gpac-nightly-builds/) is correctly added to the environment variables

### Features Added
1. Automatically package EC3 as M4A using an external MP4Box
2. Change the directory structure to `Artist Name\Album Name`; Atmos download files are moved to `AM-DL-Atmos downloads`, with the directory structure `Artist Name\Album Name [Atmos]`
3. Display overall completion status after the run
4. Automatically embed cover art and LRC lyrics (requires media-user-token, see the instructions at the end for how to obtain it)
5. Automatic builds: You can download the latest automatic build version from the [Actions](https://github.com/zhaarey/apple-music-alac-atmos-downloader/actions) page, and use `main.exe url` directly
6. `main_select` supports manually entering M3U8, using `#` for input, e.g., `#1 #2`. It also supports reading M3U8 from a TXT file by entering the TXT filename
7. `main` supports using `go run main.go "txt file address"`. The TXT filename needs a specific format, e.g., `cn_1707581102_THE BOOK 3.txt`. It is recommended to use this [Reqable script code](https://telegra.ph/Reqable-For-Apple-Music-05-01) to auto-generate
8. `main` supports `check`, where you can input a text address or an API database
9. Added `get-m3u8-from-device` option: Set to `true` and set the port with `adb forward tcp:20020 tcp:20020` to get M3U8 from an emulator
10. Supports folder and file templates
11. Supports downloading artists: `go run main.go https://music.apple.com/us/artist/taylor-swift/159260351`

### This project only supports ALAC and Atmos
- `alac (audio-alac-stereo)`
- `ec3 (audio-atmos / audio-ec3)`

### Python Project
For AAC downloads, it is recommended to use WorldObservationLog’s [AppleMusicDecrypt](https://github.com/WorldObservationLog/AppleMusicDecrypt)

[AppleMusicDecrypt](https://github.com/WorldObservationLog/AppleMusicDecrypt) supports the following encodings
- `alac (audio-alac-stereo)`
- `ec3 (audio-atmos / audio-ec3)`
- `ac3 (audio-ac3)`
- `aac (audio-stereo)`
- `aac-binaural (audio-stereo-binaural)`
- `aac-downmix (audio-stereo-downmix)`


# Apple Music ALAC / Dolby Atmos Downloader

Original script by Sorrow. Modified by me to include some fixes and improvements.

## How to use
1. Create a virtual device on Android Studio with a image that doesn't have Google APIs.
2. Install this version of Apple Music: https://www.apkmirror.com/apk/apple/apple-music/apple-music-3-6-0-beta-release/apple-music-3-6-0-beta-4-android-apk-download/. You will also need SAI to install it: https://f-droid.org/pt_BR/packages/com.aefyr.sai.fdroid/.
3. Launch Apple Music and sign in to your account. Subscription required.
4. Port forward 10020 TCP: `adb forward tcp:10020 tcp:10020`.
5. Start frida server.
6. Start the frida agent: `frida -U -l agent.js -f com.apple.android.music`.
7. Start downloading some albums: `go run main.go https://music.apple.com/us/album/whenever-you-need-somebody-2022-remaster/1624945511`.
8. Start downloading singles: `go run main_select.go https://music.apple.com/us/album/whenever-you-need-somebody-2022-remaster/1624945511` input numbers separated by spaces.
9. Start downloading some playlists: `go run main.go https://music.apple.com/us/playlist/taylor-swift-essentials/pl.3950454ced8c45a3b0cc693c2a7db97b` or `go run main.go https://music.apple.com/us/playlist/hi-res-lossless-24-bit-192khz/pl.u-MDAWvpjt38370N`.
10. For dolby atmos: `go run main_atmos.go https://music.apple.com/us/album/1989-taylors-version-deluxe/1713845538`.

[Chinese Tutorial - See Method 3](https://telegra.ph/Apple-Music-Alac高解析度无损音乐下载教程-04-02-2)

## Downloading lyrics
1. Open [Apple Music](https://music.apple.com) and log in
2. Open the Developer tools, Click `Application -> Storage -> Cookies -> https://music.apple.com`
3. Find the cookie named `media-user-token` and copy its value
4. Paste the cookie value obtained in step 3 into the config.yaml and save it
5. Start the script as usual
