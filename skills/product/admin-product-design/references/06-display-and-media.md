# 06 — Date, Number, Money, Media Upload, and Display

## Load when

Use for any date/time, number, amount, unit, percentage, image, video, audio, upload, preview, or thumbnail behavior.

## Date and time

| Item | Rule |
|---|---|
| Date | `YYYY-MM-DD` |
| Date-time | `YYYY-MM-DD HH:mm`, 24-hour clock; add `:ss` only when seconds are required. |
| Range | `开始时间 至 结束时间`, inclusive of both boundaries. |
| Relative time | Only for messages/activity: `< 1h` → `x 分钟前`; `< 24h` → `x 小时前`; otherwise absolute time. |
| Duration | `x 小时` / `x 分钟` / `x 天` by magnitude; less than one hour in minutes; empty → `-`. |
| Time zone | Beijing time. |

## Numbers, money, and units

| Item | Rule |
|---|---|
| Integer | Thousands separators above three digits, e.g. `12,345`. Applies to tokens and counts too. |
| Money | Thousands separators + two decimals + unit, e.g. `12,345.00 元`; zero → `0.00`; integer amounts may omit decimals, e.g. `¥29,800`. |
| Large amounts | Use 万/亿 with a unit and one consistent conversion across the page; never mix 元 and 万元 in one view. |
| Negative | Sign before the digits, e.g. `-1,234.00 元`. |
| Percentage | Two decimals, e.g. `12.35%`. |
| Empty value | `-`; never `0`, `null`, or blank. Keep the same rule in exports. |
| Column unit | Put a uniform unit in the header (`金额（元）`) and omit it from cells. |
| Mixed units | Show the unit with each cell value. |
| Input unit | Place the unit inside or at the fixed trailing edge of the input. |

## Image upload

| Item | Rule |
|---|---|
| Formats | JPG, PNG, WebP; PNG when transparency is needed. |
| Per-file size | **DEFAULT/PENDING:** 10 MB; confirm before presenting as final. |
| Batch count | **DEFAULT/PENDING:** at most 9 images; block excess files in the frontend. |
| Single-image contexts | **DEFAULT:** editor images, ID documents, and similar contexts accept one file only; document exceptions. |
| Compression | **DEFAULT:** compress files over 2 MB in the browser without noticeable quality loss. |
| Aspect ratio | Avatar `1:1`; cover `16:9`; detail images unrestricted; provide cropping when required. |
| Thumbnails | Use thumbnails in lists and previews; open the original on click; never render full originals in list rows. |

## Video and audio

| Item | Rule |
|---|---|
| Video format | MP4 / H.264. MOV support or transcoding is **PENDING**. |
| Embedded video | **MUST:** allow only whitelisted domains; block all others with a clear message. List the whitelist in the PRD. |
| Size / duration | **DEFAULT/PENDING:** 100 MB / 5 minutes; confirm per feature. |
| Cover | First frame by default; user may choose another frame. |
| Playback | Muted, no autoplay; click to play; pause, seek, and fullscreen supported. |
| Audio attachments | Common formats such as MP3/WAV; exact format and ≤20 MB are **PENDING**. |

## Upload and display interaction

- **MUST:** show upload progress.
- **MUST:** on failure, show the reason and allow retrying that file without clearing successful files.
- **MUST:** invalid format or size is blocked immediately, before upload; copy states the exact limit.
- **MUST:** preview supports zoom, next/previous for multiple images, and download where relevant.
- **MUST:** deleting a file requires confirmation.
- **MUST:** failed image load shows a standard fallback with retry; loading shows a placeholder.
- **MUST:** define empty, uploading, success, failure, and deleted states.

## Required PRD output

- Date/time formats and time zone, including relative-time rules.
- Money/number/percentage precision, units, separators, and empty values.
- Image/video/audio formats, limits, compression, aspect ratio, and thumbnails.
- Upload states, retry behavior, validation copy, preview, delete, and fallback.
- Deviations and `PENDING` thresholds under `差异点` / `TBD`.

## Validation checklist

- [ ] Format and precision examples are concrete.
- [ ] Units are consistent across list, detail, and export.
- [ ] Upload limits match backend and frontend enforcement.
- [ ] Failure and retry paths preserve successful files.
- [ ] Media has empty/loading/error states.
- [ ] All `PENDING` limits are visibly marked.