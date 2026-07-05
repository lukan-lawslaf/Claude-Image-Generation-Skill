# ?? Claude Image Generation Skill

A plug-and-play **Claude agent skill** that generates stunning images from plain English descriptions — powered by [Pollinations AI](https://pollinations.ai/). **No API key required.**

---

## ? What It Does

This skill supercharges Claude with the ability to **generate, enhance, and display images** on demand. Just ask naturally — Claude will:

1. **Understand your intent** — detect image requests even without the word "image"
2. **Enhance your prompt** — rewrites vague requests into vivid, detailed prompts optimized for AI image generation
3. **Generate the image** — calls Pollinations AI's free, keyless endpoint
4. **Display the result** — embeds the image inline in the chat *and* saves a downloadable copy

---

## ?? Features

| Feature | Details |
|---|---|
| ?? No API key | Uses [Pollinations AI](https://image.pollinations.ai) — completely free |
| ?? Smart prompt enhancement | Adds lighting, style, composition, atmosphere automatically |
| ?? Adaptive sizing | Picks portrait / landscape / square based on the use case |
| ?? Random seeds by default | Every run produces a fresh image unless you want reproducibility |
| ?? Iteration support | Fix the seed to refine the same image across multiple prompts |
| ??? Inline + downloadable | Shows in chat *and* saves a local file |

---

## ?? Installation

### 1. Clone or download this repo

```bash
git clone https://github.com/lukan-lawslaf/Claude-Image-Generation-Skill.git
```

### 2. Place the skill folder in your Claude agent's skills directory

```
your-agent/
+-- skills/
    +-- image-generator/       ? drop this folder here
        +-- SKILL.md
        +-- scripts/
            +-- generate_image.py
```

Or install directly as a `.skill` file if your agent runner supports it.

### 3. That's it — no dependencies, no API keys

The script uses only Python standard library (`urllib`, `argparse`, `random`, `re`). Python 3.6+ is all you need.

---

## ?? Usage Examples

Just talk to Claude naturally. Any of these will trigger image generation:

```
Draw me a dragon over Tokyo at night
Generate a wallpaper of a cozy cabin in a snowy forest
I need an icon of a lightning bolt
What would a futuristic city look like?
Can I get a pic of a golden retriever on a beach?
```

Claude will enhance your prompt, generate the image, and display it inline.

### Explicit size requests

```
Portrait photo of a samurai warrior    ? 768 × 1024
Desktop wallpaper of an aurora         ? 1920 × 1080
App icon of a fire emoji, pixel art    ? 512 × 512
```

---

## ??? How It Works

### Skill trigger (`SKILL.md`)

The `SKILL.md` file contains the skill metadata and detailed instructions for Claude. It tells the agent:
- **When** to activate (any image/picture/visual request)
- **How** to enhance prompts
- **Which dimensions** to pick for different use cases
- **How** to display results

### Script (`scripts/generate_image.py`)

A lightweight Python script that:

1. URL-encodes the enhanced prompt
2. Builds the Pollinations AI endpoint URL
3. Downloads the image bytes to a local file
4. Prints `URL:` and (if download succeeded) `FILE:` lines for Claude to consume

```bash
# Basic usage
python3 scripts/generate_image.py "A futuristic city at dusk" --width 1024 --height 768

# With explicit seed (for reproducible/iterable results)
python3 scripts/generate_image.py "A futuristic city at dusk" --seed 42

# Save to a specific path
python3 scripts/generate_image.py "A futuristic city at dusk" --out ~/Desktop/city.png

# URL only (no download)
python3 scripts/generate_image.py "A futuristic city at dusk" --no-download
```

**Output format:**
```
URL: https://image.pollinations.ai/prompt/A%20futuristic%20city%20at%20dusk?width=1024&height=768&nologo=true&seed=1837291
FILE: /path/to/saved/image.png   <- only printed if download succeeded
```

---

## ?? Sizing Guide

| Use case | Dimensions |
|---|---|
| General / unspecified | 1024 × 1024 |
| Portrait, character art, phone wallpaper | 768 × 1024 |
| Landscape, scenery, desktop wallpaper | 1024 × 768 |
| Widescreen banner | 1920 × 1080 |
| Icon, avatar, small asset | 512 × 512 |

---

## ?? Prompt Enhancement Examples

| User says | Enhanced prompt sent to API |
|---|---|
| `cat astronaut` | *Cute orange cat astronaut standing on the moon wearing a futuristic spacesuit, Earth visible in the background, cinematic lighting, ultra detailed digital art, masterpiece, vibrant colors, 8k.* |
| `dragon over tokyo` | *Epic fantasy artwork of a gigantic glowing dragon flying above futuristic Tokyo at night, neon signs illuminating the city, dramatic clouds, volumetric lighting, cinematic composition, highly detailed digital painting, masterpiece, 8k.* |

---

## ?? File Structure

```
image-generator/
+-- README.md                  ? you are here
+-- SKILL.md                   ? Claude skill definition & instructions
+-- scripts/
    +-- generate_image.py      ? Pollinations URL builder + downloader
```

---

## ?? Powered By

- [**Pollinations AI**](https://pollinations.ai/) — free, open, no-key image generation API
- Built for use with **Claude** (Anthropic) agent frameworks that support the `.skill` / `SKILL.md` convention

---

## ?? License

MIT — free to use, modify, and distribute.
