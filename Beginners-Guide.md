# yt-dlp Beginners Guide
*A simple quick-start guide for new users of yt-dlp.*

This guide is designed for beginners who want to **install yt-dlp**, **download videos quickly**, and **use the most commonly needed options**, without reading the full manual.

For advanced usage, see the main README and the Wiki.

**Helpful Wiki Pages for Beginners:**  
- [FAQ — Common Misunderstandings](https://github.com/yt-dlp/yt-dlp-wiki/blob/master/FAQ.md)  
- [Installation Guide](https://github.com/yt-dlp/yt-dlp-wiki/blob/master/Installation.md)  

> This page is a quick-start guide only.
> For authoritative, complete documentation, please refer to the main README.

---

## 1. What is yt-dlp?

yt-dlp is a command-line downloader for **videos and audio** from **YouTube** and **thousands of sites**.

It features:

- Video and audio download from supported sites
- Subtitles  
- Playlist support  
- SponsorBlock integration  
- Format selection  
- Post-processing  
- Authentication support  

This guide covers **only the basics**.

---

## 2. Installation (Beginner Friendly)

### **Windows**

1. Download:  
   https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp.exe  

2. Run:

```bash
yt-dlp.exe "<URL>"
```

---

### **macOS**
```bash
brew install yt-dlp
```
Or:
```bash
pip3 install -U yt-dlp
```

---

### **Linux**

```bash
sudo apt install yt-dlp
```

Or:

```bash
pip3 install -U yt-dlp
```

### Linux package managers (apt, dnf, etc.) may be outdated

Some distributions may **not package the latest version**.  
If you need the newest release, install via pip or the standalone binary:

```bash

curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -o yt-dlp

chmod +x yt-dlp

sudo mv yt-dlp /usr/local/bin/

```

Or install with pip:

```bash

pip3 install -U yt-dlp

```

Arch Linux users (pacman) usually get up‑to‑date builds.


> If the command cannot be found, ensure that the installation directory is in PATH.
> See [Installation.md](https://github.com/yt-dlp/yt-dlp-wiki/blob/master/Installation.md) for platform-specific notes.

## 3. First Steps — Basic Commands

These commands cover the commonly used basic operations.

### Download a video
```bash
yt-dlp "<URL>"
```

### Download audio only (MP3)
```bash
yt-dlp -x --audio-format mp3 "<URL>"
```

### List available formats
```bash
yt-dlp -F "<URL>"
```

### Download a specific format
```bash
yt-dlp -f 137+140 "<URL>"
```

### Download a playlist
```bash
yt-dlp "<playlist_url>"
```

---

## 4. Useful Features for Beginners

### Download subtitles
```bash
yt-dlp --write-subs --sub-langs "en.*" "<URL>"
```

### Embed subtitles
```bash
yt-dlp --embed-subs "<URL>"
```

### Remove sponsored segments (SponsorBlock)
```bash
yt-dlp --sponsorblock-remove all "<URL>"
```


### Custom Output Filenames
yt-dlp supports output templates.  
Beginners who want customized filenames should refer to the “Output Template” section of the main [README](https://github.com/yt-dlp/yt-dlp/blob/master/README.md).

Example:

```bash
yt-dlp -o "%(title)s.%(ext)s" "<URL>"
```

---

## 5. Beginner-Friendly Examples

| Purpose | Command |
|--------|---------|
| Download MP4 formats | `yt-dlp -S "ext:mp4" "<URL>"` |
| Convert to mp3 | `yt-dlp -x --audio-format mp3 "<URL>"` |
| Playlist | `yt-dlp "<playlist>"` |
| Get subtitles | `yt-dlp --write-subs "<URL>"` |
| Show formats | `yt-dlp -F "<URL>"` |
| Windows-safe filename | `yt-dlp --restrict-filenames "<URL>"` |

---

## 6. Common Download Scenarios (YouTube, Livestreams, Members-only, Subtitles, Quality)

### YouTube — Select MP4 formats (when available)
```bash
yt-dlp -S "res,ext:mp4" "<YouTube URL>"
```

### YouTube — Download Specific Resolution (e.g., 1080p)
```bash
yt-dlp -S "res:1080" "<YouTube URL>"
```

### YouTube — Download Only Audio (MP3)
```bash
yt-dlp -x --audio-format mp3 "<YouTube URL>"
```

---

### Livestream — Download Ongoing Stream
```bash
yt-dlp "<live URL>"
```

### Livestream — Attempt to Start from Beginning
Some sites provide a rewindable buffer for livestreams.  

`--live-from-start` is supported only by a small number of extractors that provide a rewindable buffer.

```bash
yt-dlp --live-from-start "<live URL>"
```

---

### Members-only Video (Age-restricted / Private / Channel Membership)

These require authentication. The most common method is using browser cookies.

Note:

- Cookie extraction is **not supported on all platforms** (e.g., limited support on Windows).

- Chrome-based extraction has limited support on Windows; see the [README](https://github.com/yt-dlp/yt-dlp/blob/master/README.md) for platform notes.  

- Users who need more information about cookies should refer to the “Authentication” section of the main [README](https://github.com/yt-dlp/yt-dlp/blob/master/README.md).


Example:

```bash
yt-dlp --cookies-from-browser firefox "<YouTube Members-only URL>"
```

If multiple profiles exist:

```bash
yt-dlp --cookies-from-browser "firefox:Profile 1" "<URL>"
```

---

### Download Subtitles Only
```bash
yt-dlp --skip-download --write-subs "<URL>"
```

### Auto-generated Subtitles (if provided by the site)
Some sites provide auto-generated subtitles; some do not.

```bash
yt-dlp --write-auto-subs "<URL>"
```

### Download Subtitles in Specific Languages
```bash
yt-dlp --write-subs --sub-langs "en,ja" "<URL>"
```

---

### Highest Audio Quality Available
```bash
yt-dlp -f "ba" "<URL>"
```

### Force WebM / MP4 Only
WebM:
```bash
yt-dlp -S "ext:webm" "<URL>"
```

MP4:
```bash
yt-dlp -S "ext:mp4" "<URL>"
```

## 6.1 Using a Proxy (optional)

yt-dlp can use a proxy:

HTTP:

```bash
yt-dlp --proxy "http://127.0.0.1:8080" "<URL>"
```
For more information, see the [FAQ](https://github.com/yt-dlp/yt-dlp-wiki/blob/master/FAQ.md)
```

---

## 7. Common Issues & Fixes

### ffmpeg not found
Install ffmpeg:

macOS:
```bash
brew install ffmpeg
```

Ubuntu:
```bash
sudo apt install ffmpeg
```

Windows: download from the official FFmpeg website.

---

### Unsupported URL
Check supported sites: [supportedsites.md](https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md)

---

### Subtitles missing
```bash
yt-dlp --list-subs "<URL>"
```

---

### Slow download

> See [FAQ](https://github.com/yt-dlp/yt-dlp-wiki/blob/master/FAQ.md) for notes about download speed.

---

---

## 8. Tips for New Users

* Always wrap URLs in quotes  
Use `-v` for debugging  
```bash
yt-dlp -v "<URL>"
```
* Choose a download folder:
```bash
yt-dlp -P "~/Downloads" "<URL>"
```
* Put yt-dlp in PATH to use it anywhere  

---

## 9. When Should You Read the Full README?

Read the main README if you need:

- All command options  
- Full format selection  
- Advanced metadata features  
- Post-processing  
- Authentication  
- Plugins  


> This beginner guide is **not** meant to replace the full documentation.

---
