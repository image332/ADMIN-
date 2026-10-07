# VIDEO & MUSIC DOWNLOADS — Admin Edition

A Pyrogram + yt-dlp + FFmpeg Telegram downloader. It supports public media URLs from many yt-dlp extractors, including TikTok, YouTube/Shorts, Instagram, Facebook video/reels (when the extractor can access the media), X/Twitter, Reddit, Pinterest and more.

## User flow
1. `/start` shows a configurable welcome message/photo and a clean reply keyboard.
2. User taps **📥 Download**.
3. Bot asks for the URL.
4. Bot scans the URL and shows Video / Audio.
5. Video → bot reads the actual available video resolutions and shows buttons such as 1080p/720p/480p/360p.
6. Audio → bot sends high-quality MP3.
7. Caption automatically uses the media title, uploader/channel when available, source extractor and file size. It does not invent a username.

## Admin controls
Set `ADMIN_IDS` in `.env`.

- `/admin` — control panel
- `/welcome_text text` — welcome text
- `/welcome_photo_on` then send a direct image URL — enable/save welcome image
- `/welcome_photo_off` — disable image
- `/welcome_button Name | https://example.com` — custom welcome button
- `/welcome_channel Name | https://t.me/channel` — channel button
- `/force_on`, `/force_off` — force join
- `/force_channel @channel` — channel to check (bot must be able to check membership)
- `/force_url https://t.me/channel` — join URL
- `/force_text text` — force-join message
- `/force_button text` — force-join button label
- `/ban USER_ID`, `/unban USER_ID` — user moderation
- Admin panel → Stats / Settings / Welcome / Force Join / Broadcast / Ban / Unban

Settings are stored in SQLite (`bot.db`) so they persist across restarts. On Render, attach a persistent disk if you need SQLite settings and downloads to survive service restarts.

## Facebook note
Use an actual public Facebook video/reel URL. A normal text/photo post that contains lyrics or text is not necessarily a downloadable video and can legitimately return `Unsupported or unavailable URL`.

## Cookies
This build does not require browser cookies. Some websites, especially some YouTube media, may require authentication or verification; those URLs are reported as unavailable instead of crashing the bot.

## Render Web Service
The app starts a health server on Render's `PORT` while Pyrogram runs. Use the included Dockerfile or Python runtime. The included Dockerfile installs FFmpeg and Node.js.

Required environment variables: `API_ID`, `API_HASH`, `BOT_TOKEN`, `ADMIN_IDS`.
