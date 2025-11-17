# yt-dlp Beginners Guide
*A simple quick-start guide for new users of yt-dlp.*

This guide is designed for beginners who want to **install yt-dlp**, **download videos quickly**, and **use the most commonly needed options**, without reading the full manual.

For advanced usage, see the main README and the Wiki.

**Helpful Wiki Pages for Beginners:**  
- [FAQ — Common Misunderstandings]( https://github.com/yt-dlp/yt-dlp-wiki/blob/master/FAQ.md )  
- [Installation Guide]( https://github.com/yt-dlp/yt-dlp-wiki/blob/master/Installation.md )  

---

## 1. What is yt-dlp?

yt-dlp is a command-line downloader for **videos and audio** from **YouTube** and **thousands of sites**.

It features:

- Best-quality download  
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

---

## 2.1 Installation Troubleshooting (PATH, curl, .profile, config directory)

Many beginners struggle with installation because some steps that are “obvious” to developers are *not obvious at all*.  
This section addresses the most common issues.

---

### A. “yt-dlp: command not found”
This means your system cannot find the program.  
You must add yt-dlp to your **PATH**.

### macOS / Linux
If you downloaded the binary manually:

```bash
chmod +x yt-dlp
sudo mv yt-dlp /usr/local/bin/
```

If you installed with pip:

```bash
pip3 install -U yt-dlp
```

If the command still does not work:

```bash
echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.profile
source ~/.profile
```

---

### B. Understanding `.profile` and PATH
Your shell only searches folders listed in `PATH`.

View your current PATH:
```bash
echo $PATH
```

If yt-dlp is not inside any listed folder, add it manually:

```bash
echo 'export PATH="/usr/local/bin:$PATH"' >> ~/.profile
source ~/.profile
```

---

### C. “curl command not found” (macOS / Linux)
Install curl:

macOS:
```bash
brew install curl
```

Ubuntu:
```bash
sudo apt install curl
```

---

### D. Installing with curl (full example)
Many beginners do not know how to use `curl`.  
Here is a working example:

```bash
curl -L https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp \
    -o yt-dlp
chmod +x yt-dlp
sudo mv yt-dlp /usr/local/bin/
```

You can now run:
```bash
yt-dlp "<URL>"
```

---

### E. Where to place the configuration file (`yt-dlp.conf`)
Beginners are often confused about where the config file belongs.

Use:

**Linux / macOS**  
```
~/.config/yt-dlp/config
```

**Windows**  
```
%APPDATA%\yt-dlp\config.txt
```

Create the folder manually if it does not exist.

You may place default options there, for example:

```
--embed-subs
--embed-metadata
--sponsorblock-remove all
```

yt-dlp will use these options **automatically** every time.

---

### F. Verify installation
```bash
yt-dlp --version
```

If this prints a version number, installation succeeded.

## 3. First Steps — Basic Commands

These commands cover **90% of beginner use cases**.

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

### Use browser cookies (age-restricted videos)
```bash
yt-dlp --cookies-from-browser chrome "<URL>"
```

### Custom output filename
```bash
yt-dlp -o "%(title)s.%(ext)s" "<URL>"
```

---

## 5. Beginner-Friendly Examples

| Purpose | Command |
|--------|---------|
| Best MP4 | `yt-dlp -S "ext:mp4" "<URL>"` |
| Best audio (mp3) | `yt-dlp -x --audio-format mp3 "<URL>"` |
| Playlist | `yt-dlp "<playlist>"` |
| Get subtitles | `yt-dlp --write-subs "<URL>"` |
| Show formats | `yt-dlp -F "<URL>"` |
| Windows-safe filename | `yt-dlp --restrict-filenames "<URL>"` |

---

## 6 Common Download Scenarios (YouTube, Livestreams, Members-only, Subtitles, Quality)

### YouTube — Best Quality MP4
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

### ivestream — Start from Beginning (if supported)
```bash
yt-dlp --live-from-start "<live URL>"
```

---

### Members-only Video (Age-restricted / Private / Channel Membership)
> Requires browser cookies.

```bash
yt-dlp --cookies-from-browser chrome "<YouTube Members-only URL>"
```

If multiple profiles exist:

```bash
yt-dlp --cookies-from-browser "chrome:Profile 1" "<URL>"
```

---

### Download Subtitles Only
```bash
yt-dlp --skip-download --write-subs "<URL>"
```

### Download Auto-generated Subtitles
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
Check supported sites:  
https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md

---

### Slow download
```bash
yt-dlp --concurrent-fragments 8 "<URL>"
```

---

### Subtitles missing
```bash
yt-dlp --list-subs "<URL>"
```

---

## 8. Tips for New Users

✔ Always wrap URLs in quotes  
✔ Use `-v` for debugging  
```bash
yt-dlp -v "<URL>"
```
✔ Choose a download folder:
```bash
yt-dlp -P "~/Downloads" "<URL>"
```
✔ Put yt-dlp in PATH to use it anywhere  

---

## 9. When Should You Read the Full README?

Read the main README if you need:

- All command options  
- Full format selection  
- Advanced metadata features  
- Post-processing  
- Authentication  
- Plugins  

This beginner guide is **not** meant to replace the full documentation.

---

## 10. Top 10 Beginner Mistakes (and how to avoid them)

1. **Not installing ffmpeg**  
   yt-dlp can download videos without it, but cannot merge formats or extract audio.  
   → Install ffmpeg early.

2. **Forgetting to use quotes around URLs**  
```bash
yt-dlp https://youtu.be/...   # ❌ wrong on some shells
```
```bash
yt-dlp "https://youtu.be/..." # ✔ correct
```

3. **Confusing “format code” with “resolution text”**  
Use `yt-dlp -F "<URL>"` to get actual codes like `137`, not “1080p”.

4. **Expecting MP4 when YouTube only provides WebM**  
Some qualities only exist in WebM.  
→ Use: `-S "ext:mp4"` to force MP4 selection.

5. **Using outdated `youtube-dl` flags**  
yt-dlp syntax differs in some areas—always check README sections “Differences in Default Behavior”.

6. **Thinking audio-only downloads include thumbnails**  
`-x` extracts only audio; thumbnails require: `--embed-thumbnail`.

7. **Expecting auto-generated subtitles for every site**  
Some websites do *not* provide auto captions.  
→ Check with: `--list-subs`.

8. **Not understanding why Members-only videos fail**  
These require authenticated cookies.  
→ Use: `--cookies-from-browser chrome`.

9. **Expecting livestream rewind when the platform does not support it**  
`--live-from-start` works only when the platform offers a full timeline buffer.

10. **Overwriting files unintentionally**  
Use custom output templates:  
```bash
yt-dlp -o "%(title)s-%(id)s.%(ext)s"
```

---

## 11. About This Guide

This guide helps new users start quickly **without being overwhelmed**.  
It intentionally keeps things simple.  
Contributions for clarity or more examples are welcome.