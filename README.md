### !! You must first install [MP4Box](https://gpac.io/downloads/gpac-nightly-builds/), and ensure that [MP4Box](https://gpac.io/downloads/gpac-nightly-builds/) is correctly added to the environment variables.

### Added Features
1. Automatically invokes external MP4Box to encapsulate EC3 into M4A.
2. Changes directory structure to `Artist Name\Album Name`; Atmos download files are moved to `AM-DL-Atmos downloads`, with the structure `Artist Name\Album Name [Atmos]`.
3. Displays overall completion status after the operation.
4. Automatically embeds cover art and LRC lyrics (requires media-user-token; see the final instructions for how to obtain it).
5. Auto-build available at [Actions](https://github.com/zhaarey/apple-music-alac-atmos-downloader/actions). You can download the latest auto-build version and run directly using `main.exe url`.
6. `main` supports `check`, which can accept text addresses or an API database.
7. Added `get-m3u8-from-device`. Set this to true and configure the port `adb forward tcp:20020 tcp:20020` to fetch m3u8 from the emulator.
8. Folder and file templates are supported.
9. Supports downloading artist albums with `go run main.go https://music.apple.com/us/artist/taylor-swift/159260351` and `--all-album` to automatically select all albums by the artist.
10. Added [wrapper](https://github.com/zhaarey/wrapper/releases) mode (currently only runs on Linux). The decryption speed is incredibly fast, almost instantaneous.
11. `limit-max` supports length restrictions, defaulting to 200.
12. Supports both word-by-word and unsynced lyrics.

This project only supports ALAC and Atmos:
- `alac (audio-alac-stereo)`
- `ec3 (audio-atmos / audio-ec3)`

### Python Project
To download AAC, it is recommended to use WorldObservationLog's [AppleMusicDecrypt](https://github.com/WorldObservationLog/AppleMusicDecrypt).

[AppleMusicDecrypt](https://github.com/WorldObservationLog/AppleMusicDecrypt) supports the following codecs:
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
8. Start downloading singles: `go run main.go --select https://music.apple.com/us/album/whenever-you-need-somebody-2022-remaster/1624945511` input numbers separated by spaces.
9. Start downloading some playlists: `go run main.go https://music.apple.com/us/playlist/taylor-swift-essentials/pl.3950454ced8c45a3b0cc693c2a7db97b` or `go run main.go https://music.apple.com/us/playlist/hi-res-lossless-24-bit-192khz/pl.u-MDAWvpjt38370N`.
10. For dolby atmos: `go run main.go --atmos https://music.apple.com/us/album/1989-taylors-version-deluxe/1713845538`.

[Chinese Tutorial](https://telegra.ph/Apple-Music-Alac高解析度无损音乐下载教程-04-02-2)

## Downloading lyrics
1. Open [Apple Music](https://music.apple.com) and log in
2. Open the Developer tools, Click `Application -> Storage -> Cookies -> https://music.apple.com`
3. Find the cookie named `media-user-token` and copy its value
4. Paste the cookie value obtained in step 3 into the config.yaml and save it
5. Start the script as usual
