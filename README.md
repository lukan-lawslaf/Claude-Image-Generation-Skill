# Claude Image Generation Skill

![Python](https://img.shields.io/badge/Python-3.6%2B-blue?logo=python)
![No API Key](https://img.shields.io/badge/API%20Key-None%20Required-brightgreen)
![License](https://img.shields.io/badge/License-MIT-green)
![Powered By](https://img.shields.io/badge/Powered%20By-Pollinations%20AI-ff69b4)

> A plug-and-play Claude agent skill that generates images from plain English — no API key, no setup, no dependencies beyond Python's standard library.

---

## How It Works

1. You make any image request — casual phrasing like *"draw me a fox"* or *"what would a neon Tokyo street look like?"* all trigger it.
2. Claude enhances your prompt automatically, adding lighting, style, composition, and atmosphere details.
3. `scripts/generate_image.py` builds a [Pollinations AI](https://pollinations.ai/) URL and downloads the image locally.
4. Claude displays it inline and optionally shows you the original vs. enhanced prompt.

No tokens spent on image generation. No rate limits. Completely free.

---

## Installation

```bash
git clone https://github.com/lukan-lawslaf/Claude-Image-Generation-Skill.git
```

Drop the folder into your Claude agent's `skills/` directory alongside `SKILL.md`. That's it.

**Requirements:** Python 3.6+ — uses only the standard library (`argparse`, `urllib`, `re`, `random`).

---

## Usage

Just ask naturally. All of these work:

```
Draw me a cozy cabin in a snowy forest at dusk
Generate a portrait of a cyberpunk samurai
What would a bioluminescent deep-sea creature look like?
Make a banner image for a space exploration startup
Create an icon for a meditation app
```

Claude picks the right dimensions automatically based on what you're making.

---

## Size Presets

| Use Case | Dimensions | Aspect Ratio |
|---|---|---|
| General / Square | 1024 × 1024 | 1:1 |
| Portrait / Character art | 768 × 1024 | 3:4 |
| Landscape / Scene | 1024 × 768 | 4:3 |
| Widescreen / Banner | 1920 × 1080 | 16:9 |
| Icon / Thumbnail | 512 × 512 | 1:1 |

You can also specify custom dimensions: *"make a 1200×630 image for an Open Graph card"*.

---

## Prompt Enhancement

Claude rewrites vague prompts before passing them to the generator:

| Your request | What gets sent |
|---|---|
| `a sunset` | `golden hour sunset over calm ocean, warm amber and rose tones, soft lens flare, cinematic composition, photorealistic` |
| `a robot` | `sleek humanoid robot in a dimly lit laboratory, chrome surfaces with blue LED accents, detailed mechanical joints, dramatic side lighting, concept art style` |

Already-detailed prompts get only light polish — Claude won't change your subject or override a style you've specified.

---

## Script Reference

`scripts/generate_image.py` can also be run directly:

```bash
python3 scripts/generate_image.py "prompt text" \
  --width 1024 \
  --height 1024 \
  --seed 42 \
  --out my_image.png
```

| Argument | Default | Description |
|---|---|---|
| `prompt` | *(required)* | The image-generation prompt |
| `--width` | `1024` | Output width in pixels |
| `--height` | `1024` | Output height in pixels |
| `--seed` | random | Fixed seed for reproducible results |
| `--out` | `<slug>.png` | Output file path |
| `--no-download` | off | Print URL only, skip download |

**Output format:**
```
URL: https://image.pollinations.ai/prompt/...
FILE: /path/to/saved/image.png
```

If the download fails (e.g. no network access), the `URL:` line is still printed so Claude can embed it as a Markdown image instead.

---

## Seeds

- **Default:** random seed each run — every generation is unique.
- **Fixed seed:** pass `--seed <n>` to iterate on the same concept (tweak the prompt without changing the composition entirely).

---

## License

MIT — free to use, modify, and redistribute.

---

*Powered by [Pollinations AI](https://pollinations.ai/) — free, open, no-key image generation.*
