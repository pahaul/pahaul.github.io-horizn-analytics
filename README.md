# Horizn Analytics

A pipeline that scrapes a brand's website, extracts visual and emotional signals using structured analytical frameworks, and assembles them into structured AI image generation prompts.

Built as a proof of concept using [Horizn Studios](https://horizn-studios.com) as the target brand.

→ **[Read the article](https://pahaul.github.io/horizn-analytics/)**

---

## What it does

1. **Scrapes** selected pages of a Shopify storefront (Playwright + BeautifulSoup)
2. **Analyses text** chunks against Kansei Engineering, Geneva Emotion Wheel, IPTC NewsCodes, and Sinus-Milieus frameworks
3. **Analyses images** for photographic signals: shot size, lighting, composition, color, narrative style
4. **Aggregates** all signals into a structured brand profile with confidence scoring
5. **Generates** FLUX-optimised image prompts from the profile, with frequency-weighted random slot selection

## Stack

- Python 3.11, Ollama, Gemma 31B (cloud)
- Playwright, BeautifulSoup
- FastAPI (optional wrapper)
- Nano Banana 2 via ComfyUI for image generation

## Usage

```bash
# Full pipeline run
python pipeline.py

# Skip vision analysis
python pipeline.py --skip-vision

# Generate image prompts
python build_prompt.py

# Brand chat CLI
python brand_chat.py
```

## Structure

```
pipeline.py          — orchestrator
schemas.py           — Pydantic models
ollama_client.py     — text analysis (Pass 1a + Pass 2)
vision_client.py     — vision analysis (Pass 1b)
aggregator.py        — signal aggregation
build_context.py     — builds brand_context.xml
brand_chat.py        — CLI chat interface
build_prompt.py      — prompt generator
criteria/            — analytical framework definitions
output/              — pipeline outputs (gitignored)
```

## Output example

```
brand_profile.json — Kansei profile
────────────────────────────────────────────
modern_traditional     modern        36.5
premium_accessible     premium       38.3
rough_refined          refined       23.4
profile_confidence     0.844
```
