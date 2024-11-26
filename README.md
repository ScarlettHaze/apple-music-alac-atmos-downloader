### Prerequisites

1. Install [MP4Box](https://gpac.io/downloads/gpac-nightly-builds/) and ensure that [MP4Box](https://gpac.io/downloads/gpac-nightly-builds/) is correctly added to your system's environment variables.

---

### Features

1. **Automatically Package EC3 into M4A**
   - Uses external MP4Box for automatic EC3 to M4A packaging.

2. **Reorganize Directory Structure**
   - Changes file structure to:  
     ```
     Artist Name\Album Name
     ```
   - For Atmos downloads, files are moved to a separate folder: `AM-DL-Atmos downloads` and organized as:  
     ```
     Artist Name\Album Name [Atmos]
     ```

3. **Completion Overview**
   - Displays overall completion status after the operation ends.

4. **Embed Artwork and LRC Lyrics**
   - Automatically embeds album covers and synchronized LRC lyrics.  
   - **Requires `media-user-token`** (instructions for obtaining it are provided at the end).

5. **Automated Builds**
   - Access the latest builds on the [Actions](https://github.com/zhaarey/apple-music-alac-atmos-downloader/actions) page.  
   - Use the command:  
     ```
     main.exe url
     ```

6. **Check Mode in `main`**
   - Supports `check` with a file address or an API database as input.

7. **Retrieve M3U8 from Device**
   - When set to `true`, with the port configured using:  
     ```
     adb forward tcp:20020 tcp:20020
     ```  
   - Retrieves M3U8 from an emulator.

8. **Folder and File Templates**
   - Fully customizable templates for naming folders and files.

9. **Artist Download Mode**
   - Download all albums from an artist using:  
     ```
     go run main.go https://music.apple.com/us/artist/artist-name/artist-id --all-album
     ```

10. **Wrapper Mode**
    - A high-speed decryption mode (currently Linux-only) for near-instant decryption.  
    - Wrapper mode can be found [here](https://github.com/zhaarey/wrapper/releases).

11. **File Length Limit**
    - Set a maximum length for files using the `limit-max` parameter (default: 200).

12. **Synchronized and Unsynchronized Lyrics**
    - Supports both synchronized per-word lyrics and unsynchronized lyrics.

13. **ARM64 Decryption Support**
    - Now fully supports ARM64 architecture for decryption.

---

### Supported Formats

- ALAC: `audio-alac-stereo`  
- EC3: `audio-atmos / audio-ec3`

---

### Special Thanks
- To **`chocomint`** for creating `agent-arm64.js`.

---

### Related Projects

- For AAC downloads, use **WorldObservationLog's** [AppleMusicDecrypt](https://github.com/WorldObservationLog/AppleMusicDecrypt).

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
2. Install Apple Music

   for x86 install this version of [Apple Music 3.6.0 beta4](https://www.apkmirror.com/apk/apple/apple-music/apple-music-3-6-0-beta-release/apple-music-3-6-0-beta-4-android-apk-download/). You will also need [SAI](https://f-droid.org/pt_BR/packages/com.aefyr.sai.fdroid/) to install it.

   for arm64 install the last version of [Apple Music](https://www.apkmirror.com/apk/apple/apple-music/).
   
3. Launch Apple Music and sign in to your account. Subscription required.
4. Port forward 10020 TCP: `adb forward tcp:10020 tcp:10020`.
5. Start frida server.
6. Start the frida agent:

   for  x86 `frida -U -l agent.js -f com.apple.android.music`
   
   for arm64 `frida -U -l agent-arm64.js -f com.apple.android.music`
   
   
7. Start downloading some albums: `go run main.go https://music.apple.com/us/album/whenever-you-need-somebody-2022-remaster/1624945511`.
8. Start downloading singles: `go run main.go --select https://music.apple.com/us/album/whenever-you-need-somebody-2022-remaster/1624945511` input numbers separated by spaces.
9. Start downloading some playlists: `go run main.go https://music.apple.com/us/playlist/taylor-swift-essentials/pl.3950454ced8c45a3b0cc693c2a7db97b` or `go run main.go https://music.apple.com/us/playlist/hi-res-lossless-24-bit-192khz/pl.u-MDAWvpjt38370N`.
10. For dolby atmos: `go run main.go --atmos https://music.apple.com/us/album/1989-taylors-version-deluxe/1713845538`.

[Chinese Tutorial - See Method 3](https://telegra.ph/Apple-Music-Alac高解析度无损音乐下载教程-04-02-2)

## Downloading lyrics

1. Open [Apple Music](https://music.apple.com) and log in
2. Open the Developer tools, Click `Application -> Storage -> Cookies -> https://music.apple.com`
3. Find the cookie named `media-user-token` and copy its value
4. Paste the cookie value obtained in step 3 into the config.yaml and save it
5. Start the script as usual
