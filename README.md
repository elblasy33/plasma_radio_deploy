# Aurora Waves — أمواج أورورا

**World radio, YouTube Music and your own music in one frosted-glass player for KDE Plasma 6.**
Tune in to tens of thousands of live stations, search and queue any song on YouTube Music, play your
files and playlists, and control it all from Plasma's media controller and your media keys.

<p><a href="https://github.com/elblasy33/aurora-waves/releases/latest"><img alt="Latest release" src="https://img.shields.io/github/v/release/elblasy33/aurora-waves?label=release"></a>
<img alt="Plasma 6" src="https://img.shields.io/badge/Plasma-6-54a3d8">
<img alt="License" src="https://img.shields.io/badge/license-GPL--2.0--or--later-blue"></p>

[العربية ⬇](#بالعربي) · [Install](#install) · [User guide](#user-guide) · [Troubleshooting](#troubleshooting) · [For developers](#for-developers)

<p align="center">
  <img src="docs/screenshots/en-main.png" width="30%" alt="Player (English)">
  <img src="docs/screenshots/en-disc.png" width="30%" alt="Discover world radio">
  <img src="docs/screenshots/ar-main.png" width="30%" alt="Player (Arabic)">
</p>

---

## Features

| | |
|---|---|
| 📻 **World radio** | Search tens of thousands of stations in 220+ countries from [Radio Browser](https://www.radio-browser.info) and [zeno.fm](https://zeno.fm), by name, country (A–Z or by size) and genre. Arabic searches also find Latin spellings: فيروز ↔ Fairuz, أم كلثوم ↔ Kalthom |
| 🎵 **YouTube Music** *(optional)* | Search songs, artists and albums, browse the home feed in your language, open artist and album pages, build a queue (*play next*, *add to queue*, *similar radio*), seek, and save an artist, album or playlist as a station |
| 👤 **Your account** *(optional)* | Sign in with the Google account already open in your browser to see your liked songs, playlists, history and personal recommendations. Everything works without it |
| 📁 **Your music** | Local files, whole folders and M3U/PLS playlists, with shuffle, pause and seek |
| ➕ **Add anything** | Any stream URL (mp3/aac/m3u8), a Dailymotion or YouTube live page; one click fetches the name, description and logo |
| 🩺 **Check & repair** | Listens to every station to confirm it really carries audio, finds moved files, restores logos and suggests replacement links already tested for sound |
| 🎛 **MPRIS** | Media controller, audio visualizers, lock screen and media keys, with song title and cover art |
| 📐 **Responsive** | Wide, normal, short, tiny and narrow layouts, on a panel or on the desktop |
| 🌐 **Multilingual** | English and Arabic with left-to-right and right-to-left layouts; easy to add more languages |

<p align="center"><img src="docs/screenshots/sizes.png" width="95%" alt="Layouts at different sizes"></p>

---

## Install

### 1. Requirements

Most of these are already on a typical Plasma desktop.

| Package | Used for |
|---|---|
| `mpv` | Playback |
| `ffmpeg` | Check & repair, which listens to each stream |
| `python3-gi` | The background service that publishes MPRIS |
| `python3-pip` | *YouTube Music only:* the one-click setup downloads its two libraries |
| `yt-dlp` | Dailymotion / YouTube live-page stations |
| `imagemagick` | *Optional:* converts `.ico` favicons into logos |

```sh
# Debian / Ubuntu / KDE neon
sudo apt install mpv ffmpeg python3-gi python3-pip yt-dlp imagemagick
# Fedora
sudo dnf install mpv ffmpeg python3-gobject python3-pip yt-dlp ImageMagick
# Arch / Manjaro
sudo pacman -S mpv ffmpeg python-gobject python-pip yt-dlp imagemagick
```

### 2. Install the widget (choose one)

**A. From Plasma (KDE Store):** right-click the desktop or a panel → **Add Widgets…** →
**Get New Widgets…** → **Download New Plasma Widgets** → search for **Aurora Waves** → **Install**.

**B. From a `.plasmoid` file:** download the latest `aurora-waves-x.y.z.plasmoid` from
[Releases](https://github.com/elblasy33/aurora-waves/releases), then:

```sh
kpackagetool6 -t Plasma/Applet -i aurora-waves-2.0.0.plasmoid
```

or use **Add Widgets… → Get New Widgets… → Install Widget From Local File…**

**C. From source:**

```sh
git clone https://github.com/elblasy33/aurora-waves.git
cd aurora-waves
./install.sh --restart
```

### 3. Add it

Right-click a panel or the desktop → **Add Widgets…** → search for **Aurora Waves** and drag it where
you want it. The first run shows a welcome screen; **Discover stations** opens the stations of your
country.

> **Coming from Aurora Radio?** Aurora Waves is the same widget, renamed. It updates in place and
> keeps your stations and settings.

### Update

- **KDE Store:** *Get New Widgets* shows an **Update** button.
- **Source:** `git pull && ./install.sh --restart`

### Uninstall

```sh
kpackagetool6 -t Plasma/Applet -r com.github.elblasy33.auroraradio
rm -f ~/.local/share/applications/aurora-radio.desktop     # media-controller icon entry
rm -rf ~/.local/share/aurora-radio ~/.cache/aurora-radio    # optional: logos, cover art, YouTube Music libraries and sign-in
```

---

## User guide

### Panel icon

| Action | Result |
|---|---|
| Left click | Open the player |
| Middle click | Play / stop |
| Mouse wheel | Volume |
| Right click | Play/stop, next station, manage stations, settings |

### The player

- Click the **big cover** or **play** to play or stop. Songs and local files pause instead of stopping.
- **⏮ / ⏭** change station, or move through the queue when YouTube Music is playing.
- Click or drag the **progress bar** to seek in songs and files.
- Keyboard: **Space** play/stop, **← / →** previous/next, **↑ / ↓** volume.
- Click a station tile to play it; **right-click** a tile to play, edit, duplicate or delete it.

### YouTube Music (♪ button)

1. The first time, press **Set up YouTube Music**. It downloads two small libraries
   (`ytmusicapi` and `yt-dlp`) into the widget's own folder: no admin rights, no system changes.
   The widget keeps its `yt-dlp` up to date by itself, because YouTube changes often.
2. Before you type, the page shows YouTube Music's **home feed** in your language.
3. Search, then pick **All / Songs / Artists / Albums**. Clicking a song plays it at once and fills
   the queue with similar songs. Artist, album and playlist pages have **Play**, **Shuffle** and
   **Save as station**.
4. **⋮** next to a song: *Play next*, *Add to queue*, *Similar radio*, *Like* (signed in), *Save as station*.
5. The **queue** button (top) lists what's coming; click any song to jump to it.

**Signing in (optional, 👤 button).** Google does not allow signing in from inside a widget, so
Aurora Waves reuses the session of a browser where you are already signed in to
music.youtube.com (Chrome, Chromium, Brave, Edge, Vivaldi, Opera or Firefox). It is read only when
you press the button, stored on your computer only (`~/.local/share/aurora-radio`, readable by you
alone), refreshed from the browser every 12 hours, and removed by **Sign out**. A manual method
(pasting request headers from the browser's developer tools) is also offered.

### Managing stations (✏️ button)

- **Discover**: the world directory. Your country is preselected; a name search covers every
  country with yours first. The country picker has a search box and **A–Z / Largest** sorting.
  **▶** gives a quick listen, **＋** adds the station.
- **New**: a *Stream link*, *File*, *Folder* or *Playlist*; **Fetch** fills in the name and logo;
  logos can be a letter or emoji, an icon, an image or the station's own.
- **Import**: every entry of an `.m3u`/`.pls` file becomes a station.
- **Egyptian public radio (Maspero)**: a curated set of official stations.
- **Check**: see below.

### Check & repair

Listens to a few seconds of every station and reports what is wrong:

| Problem | What it means | Suggested fix |
|---|---|---|
| The source refuses (401/403) | The broadcaster closed the link | A replacement from Radio Browser or zeno.fm, already tested for audio |
| Not found / unreachable / timed out | Dead link or server down | Same as above |
| No audio / silent | Connects, but no sound | Same as above |
| Path not found | A file or folder was moved | Finds it by name in your music, downloads, desktop and drives |
| Missing or online-only logo | The logo is gone or only online | Fetches it again, keeps a local copy, or uses a glass letter |

### Settings (⚙)

- **Appearance:** glass opacity, aurora background, accent color, animations, logo shape, grid or
  list, columns, category chips, equalizer, stream info, panel icon.
- **General:** language (automatic, English, العربية), MPRIS, resume on login, wheel volume step.

---

## Troubleshooting

| Symptom | What to do |
|---|---|
| YouTube Music songs stop playing | Open the ♪ page once: the widget updates its own `yt-dlp` when it is a few days old |
| Dailymotion / YouTube live stations don't play | Update the system `yt-dlp` |
| One station never plays | Run **Check** and pick the suggested replacement |
| "No signed-in YouTube account was found" | Open music.youtube.com in that browser, sign in, then try again |
| Not shown in the media controller | Enable **MPRIS** in Settings → General; make sure `python3-gi` is installed |
| A change doesn't appear after updating | `systemctl --user restart plasma-plasmashell` |
| Stop the background service | `python3 ~/.local/share/plasma/plasmoids/com.github.elblasy33.auroraradio/contents/code/radioctl.py '{"cmd":"quit"}'` |

Please report bugs at [Issues](https://github.com/elblasy33/aurora-waves/issues).

---

## For developers

```
package/
├── metadata.json              plugin id, name, version
└── contents/
    ├── config/                settings schema (main.xml) and settings pages
    ├── ui/                    QML: main.qml (state), FullView, StationEditor, DiscoverPage,
    │                          YTMusicPage, HealthPage, glass components (GlassPanel, StationLogo…)
    ├── code/
    │   ├── radiod.py          playback service: one mpv process, queues, auto-reconnect, MPRIS
    │   ├── radioctl.py        client used by the widget (unix socket, one JSON request per call)
    │   ├── sources.py         Radio Browser + zeno.fm search, countries, fetch from source, audio check
    │   ├── ytmusic.py         YouTube Music: setup, search, home, artists, albums, playlists, sign-in
    │   ├── presets.js         curated Maspero library, defaults per country, palette, glyphs
    │   └── i18n.js            translations (Arabic text is the key, EN holds English)
    └── images/                app icon and bundled station logos
```

- **Install while developing:** `./install.sh --restart`
- **Build a `.plasmoid`:** `./build.sh` → `dist/aurora-waves-<version>.plasmoid`
- **Try it in a window:** `plasmoidviewer -a package`
- **Add a language:** add a table like `EN` in `code/i18n.js` and return it from `resolve()` and `tr()`.
- **Data on disk:** `~/.local/share/aurora-radio/` holds logos, the private Python libraries for
  YouTube Music (`pylib/`) and the optional sign-in; `~/.cache/aurora-radio/` holds cover art.
  (The internal id and folders keep their original *aurora-radio* names so updates keep user data.)

### Notes

- Radio Browser and zeno.fm are community directories, so some entries go offline; **Check &
  repair** exists for exactly that.
- YouTube Music support uses the unofficial [ytmusicapi](https://github.com/sigma67/ytmusicapi) and
  [yt-dlp](https://github.com/yt-dlp/yt-dlp). It is optional, off until you set it up, and meant for
  personal listening. It is not affiliated with or endorsed by Google or YouTube.

---

## بالعربي

**أمواج أورورا: إذاعات العالم ويوتيوب ميوزك وموسيقاك في مشغّل زجاجي واحد لسطح مكتب KDE Plasma 6.**
بتسمع عشرات الآلاف من الإذاعات بث مباشر، وتدوّر على أي أغنية في يوتيوب ميوزك وتعمل لها قائمة تشغيل، وتشغّل ملفاتك وقوائمك، وكل ده بيظهر في متحكم الوسائط وأزرار الميديا.

> **كنت بتستخدم راديو أورورا؟** هو نفس الودجت باسم جديد. هيتحدّث مكانه، ومحطاتك وإعداداتك هتفضل زي ما هي.

### التثبيت
1. **المتطلبات:**
   `sudo apt install mpv ffmpeg python3-gi python3-pip yt-dlp imagemagick`
2. **الودجت:**
   - **من متجر KDE:** كليك يمين على سطح المكتب ← **إضافة عناصر واجهة** ← **احصل على عناصر جديدة** ← دوّر على **Aurora Waves**.
   - **من ملف:** نزّل `aurora-waves-x.y.z.plasmoid` من [Releases](https://github.com/elblasy33/aurora-waves/releases) وشغّل:
     `kpackagetool6 -t Plasma/Applet -i aurora-waves-2.0.0.plasmoid`
   - **من المصدر:**
     `git clone https://github.com/elblasy33/aurora-waves.git && cd aurora-waves && ./install.sh --restart`
3. **ضيفه:** من **إضافة عناصر واجهة** دوّر على **أمواج أورورا** واسحبه للوحة أو لسطح المكتب.

### الاستخدام
- **الراديو:** من ✏️ ← **اكتشف** تدوّر في إذاعات العالم (Radio Browser و zeno.fm). اختيار الدولة فيه بحث وترتيب **أبجدي** أو **الأكبر**.
- **يوتيوب ميوزك (زرار ♪):**
  - أول مرة اضغط **تفعيل يوتيوب ميوزك**. هينزّل مكتبتين صغيرتين جوه مجلد الودجت بس، من غير صلاحيات مدير.
  - قبل ما تكتب، بتظهر لك اقتراحات يوتيوب ميوزك بلغتك.
  - لما تضغط على أغنية بتشتغل على طول، وبعدها أغاني شبهها. صفحات الفنان والألبوم فيها **تشغيل** و**عشوائي** و**حفظ كمحطة**.
  - زرار **⋮** جنب الأغنية: تشغيل التالي، إضافة للقائمة، راديو مشابه، أعجبني.
- **حسابك (اختياري، زرار 👤):**
  - جوجل مش بتسمح بتسجيل الدخول من جوه الودجت، فبنستخدم حسابك المفتوح في المتصفح.
  - سجّل دخولك في music.youtube.com من المتصفح، وبعدين اختار المتصفح من الودجت.
  - هيظهر لك الأغاني اللي عجبتك وقوائمك وسجلك، والاقتراحات هتبقى على ذوقك.
  - الجلسة بتتحفظ على جهازك بس، وفيه زرار **تسجيل الخروج**.
- **فحص وإصلاح:** بيسمع كل محطة كام ثانية، ويقولك السبب لو مفيش صوت، ويقترح روابط بديلة اتجربت قبلها.
- **⚙ الإعدادات:** المظهر، وطريقة العرض، و**اللغة** (تلقائي أو العربية أو English)، وMPRIS.

### حل المشاكل
- **أغاني يوتيوب وقفت:** افتح صفحة ♪ مرة. الودجت بيحدّث نسخة `yt-dlp` بتاعته لوحده.
- **محطة مش شغالة:** شغّل **فحص** واختار البديل المقترح.
- **تعديل مش ظاهر بعد التحديث:** `systemctl --user restart plasma-plasmashell`

---

## License

GPL-2.0-or-later. See [LICENSE](LICENSE).
YouTube and YouTube Music are trademarks of Google LLC; this project is not affiliated with them.
