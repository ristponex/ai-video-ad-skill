<div align="center">

# AI Video Ad Skill

**A Claude Code skill for end-to-end video advertisement creation using Atlas Cloud**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Stars](https://img.shields.io/github/stars/thoughtincode/ai-video-ad-skill?style=social)](https://github.com/thoughtincode/ai-video-ad-skill)

Create professional video advertisements from concept to finished ad — scriptwriting, storyboarding, video generation, and multi-format export. Powered by a multi-model pipeline combining LLM, image, and video AI through Atlas Cloud's unified API.

</div>

---

## Table of Contents

- [What This Skill Does](#what-this-skill-does)
- [Features](#features)
- [Pipeline Architecture](#pipeline-architecture)
- [Prerequisites](#prerequisites)
- [API Integration Guide](#api-integration-guide)
- [Claude Code Integration](#claude-code-integration)
- [Usage Examples](#usage-examples)
- [Application Scenarios](#application-scenarios)
- [Models Used](#models-used)
- [Social Media Format Guide](#social-media-format-guide)
- [Cost Calculator](#cost-calculator)
- [API Reference](#api-reference)
- [Workflow Recipes](#workflow-recipes)
- [Troubleshooting](#troubleshooting)
- [Take This to Production](#-take-this-to-production-today)
- [License](#license)

---

## What This Skill Does

AI Video Ad Skill is a Claude Code skill that transforms how businesses create video advertisements. Instead of hiring agencies, booking studios, and waiting weeks, you describe your ad concept in natural language and the skill orchestrates multiple AI models to deliver a finished video ad.

The skill handles the entire ad creation pipeline:

1. **Scriptwriting** — Generate compelling ad scripts with DeepSeek V3.2
2. **Storyboarding** — Create visual storyboard frames with Seedream/Flux
3. **Video Generation** — Produce video clips with Kling/Seedance/Wan
4. **Multi-Format Export** — Output in platform-specific formats (16:9, 9:16, 1:1)

All powered by Atlas Cloud's API, giving you access to premium AI models at competitive pricing without managing infrastructure.

---

## Features

### Core Capabilities

- **AI Scriptwriting** — Generate ad scripts with scene descriptions, voiceover text, and timing using DeepSeek V3.2
- **Storyboard Generation** — Create visual storyboard frames from script scenes using Seedream v5.0 or Flux Dev
- **Video Clip Generation** — Produce video clips from storyboard frames or text prompts using Kling, Seedance, or Wan
- **Multi-Shot Narratives** — Create multi-scene video ads with consistent characters, settings, and visual style
- **Social Media Optimization** — Auto-format for Instagram Reels (9:16), YouTube (16:9), TikTok (9:16), Facebook (1:1)
- **A/B Testing** — Generate multiple ad versions with different models, styles, or scripts for split testing
- **Budget Flexibility** — Choose between premium (Kling v3.0 Pro), standard (Seedance), or budget (Wan 2.6) video models

### Multi-Model Pipeline

The skill chains five different AI models across three modalities:

| Stage | Model | Modality | Role | Cost |
|-------|-------|----------|------|------|
| Script | DeepSeek V3.2 | LLM | Write ad scripts with scenes, voiceover, and timing | $0.26/M tokens |
| Storyboard | Seedream v5.0 Lite | Image | Generate visual storyboard frames from scene descriptions | $0.032/image |
| Storyboard Alt | Flux Dev | Image | Budget-friendly storyboard alternative | $0.012/image |
| Video (Premium) | Kling v3.0 Pro | Video | Highest quality video generation with native audio | $0.204/video |
| Video (Standard) | Seedance v1.5 Pro | Video | Audio-visual synchronized video generation | $0.222/video |
| Video (Budget) | Wan 2.6 | Video | Cost-effective video generation | $0.07/video |

---

## Pipeline Architecture

```
                        AI Video Ad Pipeline
                        ====================

    ┌─────────────────────────────────────────────────────────────────┐
    │                        USER INPUT                               │
    │  "Create a 15-second video ad for a coffee brand"               │
    └─────────────────────┬───────────────────────────────────────────┘
                          │
                          ▼
    ┌─────────────────────────────────────────────────────────────────┐
    │                    CLAUDE CODE SKILL                             │
    │  Analyzes brief, plans pipeline, selects models                 │
    └──────┬──────────────┬───────────────────────┬───────────────────┘
           │              │                       │
           ▼              ▼                       ▼
    ┌──────────────┐ ┌──────────────┐ ┌──────────────────────┐
    │  SCRIPT      │ │  STORYBOARD  │ │     VIDEO            │
    │              │ │              │ │                      │
    │ DeepSeek V3.2│ │ Seedream v5.0│ │ Kling / Seedance /   │
    │ $0.26/M tok  │ │ $0.032/img   │ │ Wan                  │
    │              │ │              │ │                      │
    │ Ad script    │ │ Visual frames│ │ Final video clips    │
    │ with scenes, │ │ for each     │ │ with motion and      │
    │ voiceover,   │ │ scene in the │ │ audio                │
    │ and timing   │ │ script       │ │                      │
    └──────┬───────┘ └──────┬───────┘ └──────────┬───────────┘
           │                │                     │
           ▼                ▼                     ▼
    ┌─────────────────────────────────────────────────────────────────┐
    │                     OUTPUT                                      │
    │  Finished video ad ready for social media / web / TV            │
    │  Multiple formats: 16:9, 9:16, 1:1                              │
    └─────────────────────────────────────────────────────────────────┘
```

### Detailed Flow

```
  Ad Brief (text)
        │
        ▼
  ┌──────────────┐
  │ DeepSeek V3.2│  Script Generation
  │ ~500 tokens  │  "Write a 3-scene ad script for..."
  │ ~$0.0001     │
  └──────┬───────┘
         │ Script with 3 scenes
         ▼
  ┌──────────────┐
  │ Seedream v5.0│  Storyboard Generation
  │ 3 frames     │  Generate visual frame for each scene
  │ 3 x $0.032   │
  └──────┬───────┘
         │ 3 storyboard images
         ▼
  ┌──────────────┐
  │ Kling v3.0   │  Video Generation
  │ 3 clips      │  Generate 5s video for each scene
  │ 3 x $0.204   │
  └──────┬───────┘
         │ 3 video clips
         ▼
  ┌──────────────┐
  │ Final Ad     │  Total: ~$0.71
  │ 15 seconds   │  (3 scenes x 5 seconds)
  └──────────────┘
```

---

## Prerequisites

- A [Claude Code](https://claude.ai/code) installation
- An [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683) API key
- `curl` or `python3` available in your terminal (for API calls)
- Optional: `ffmpeg` for concatenating video clips into a final ad

---

## API Integration Guide

### Step 1: Get Your API Key

1. Visit [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683)
2. Create an account or sign in
3. Navigate to **API Keys** in the dashboard
4. Generate a new API key
5. First-time users get a **25% bonus** on their initial recharge (up to $100 bonus)

### Step 2: Set Environment Variable

```bash
export ATLASCLOUD_API_KEY=your_api_key_here
```

Or add it to your shell profile (`~/.bashrc`, `~/.zshrc`):

```bash
echo 'export ATLASCLOUD_API_KEY=your_api_key_here' >> ~/.zshrc
source ~/.zshrc
```

### Step 3: Verify Your Setup

```bash
curl -s https://api.atlascloud.ai/api/v1/model/list \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" | head -c 200
```

### Step 4: Install ffmpeg (Optional, for Video Concatenation)

```bash
# macOS
brew install ffmpeg

# Ubuntu/Debian
sudo apt install ffmpeg

# Windows (chocolatey)
choco install ffmpeg
```

### Step 5: Load the Skill in Claude Code

```bash
git clone https://github.com/thoughtincode/ai-video-ad-skill.git
cd ai-video-ad-skill
```

In Claude Code, run `/init` to load the skill from `SKILL.md`.

---

## Claude Code Integration

This repository is a **Claude Code skill**. Once loaded, Claude Code understands video ad creation workflows and can execute them through natural language.

### How It Works

1. Clone this repo
2. In Claude Code, run `/init` to load the skill
3. Describe the ad you want to create in plain English
4. The skill writes the script, generates storyboards, produces videos, and delivers the final ad

### Natural Language Commands

Once the skill is loaded, you can use commands like:

```
"Create a 15-second video ad for a coffee brand with morning vibes"
```

```
"Generate a product showcase video for this sneaker image"
```

```
"Create 3 social media video ads in different formats (vertical, horizontal, square)"
```

```
"Write a script and generate a video ad for our SaaS product launch"
```

Claude Code handles the entire pipeline — scripting, storyboarding, video generation, and format optimization — automatically.

---

## Usage Examples

### Example 1: Quick Coffee Brand Ad

**Prompt:**
```
Create a 15-second video ad for a coffee brand with morning vibes
```

**What the skill does:**

**Step 1 — Script (DeepSeek V3.2):**
```
Scene 1 (5s): Close-up of steam rising from a freshly poured cup of coffee on a
sunlit wooden table. Morning light streams through curtains.
Voiceover: "Every great morning starts with one thing..."

Scene 2 (5s): Hands wrapping around the warm mug, person smiling as they take
the first sip. Warm golden tones.
Voiceover: "The perfect cup, crafted just for you."

Scene 3 (5s): Wide shot of the coffee bag with brand logo, cup beside it,
morning kitchen setting. Subtle zoom in.
Voiceover: "Brand Name Coffee. Start your day right."
```

**Step 2 — Storyboard (Seedream v5.0):**
Generates 3 storyboard frames, one for each scene.

**Step 3 — Video (Kling v3.0 Pro):**
Generates 3 x 5-second video clips from storyboard frames using image-to-video.

**Total cost:** ~$0.71 (script: ~$0.001 + storyboard: $0.096 + video: $0.612)

---

### Example 2: Product Showcase Video

**Prompt:**
```
Generate a product showcase video for this sneaker image
```

**What the skill does:**
1. Takes the provided sneaker image as input
2. Uses Kling v3.0 Pro image-to-video to create a dynamic product showcase
3. Generates a 5-second clip with rotation, dramatic lighting, and smooth camera movement

**API call executed:**

```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kwaivgi/kling-v3.0-pro/image-to-video",
    "input": {
      "prompt": "Cinematic product showcase, sneaker rotating slowly on a reflective dark surface, dramatic studio lighting with color accents, premium commercial quality, smooth camera orbit",
      "image_url": "https://your-sneaker-image-url.jpg",
      "duration": 5,
      "aspect_ratio": "16:9"
    }
  }'
```

**Cost:** $0.204

---

### Example 3: Multi-Format Social Media Ads

**Prompt:**
```
Create 3 social media video ads in different formats (vertical, horizontal, square)
```

**What the skill does:**
1. Writes one ad script with DeepSeek V3.2
2. Generates storyboard frames with Seedream v5.0
3. Produces 3 video versions with different aspect ratios:
   - **Instagram Reels / TikTok:** 9:16 vertical
   - **YouTube / Website:** 16:9 horizontal
   - **Facebook Feed / Instagram Post:** 1:1 square

**API calls for video generation (3x):**

```bash
# Vertical (Instagram Reels / TikTok)
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kwaivgi/kling-v3.0-pro/image-to-video",
    "input": {
      "prompt": "Dynamic product ad, vertical format, mobile-first composition...",
      "image_url": "https://storyboard-frame-url.jpg",
      "duration": 5,
      "aspect_ratio": "9:16"
    }
  }'

# Horizontal (YouTube)
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kwaivgi/kling-v3.0-pro/image-to-video",
    "input": {
      "prompt": "Cinematic product ad, widescreen composition, dramatic framing...",
      "image_url": "https://storyboard-frame-url.jpg",
      "duration": 5,
      "aspect_ratio": "16:9"
    }
  }'

# Square (Facebook / Instagram Feed)
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kwaivgi/kling-v3.0-pro/image-to-video",
    "input": {
      "prompt": "Product ad in square format, centered composition, bold visuals...",
      "image_url": "https://storyboard-frame-url.jpg",
      "duration": 5,
      "aspect_ratio": "1:1"
    }
  }'
```

**Cost:** 3 x $0.204 = $0.612 (video only) + script + storyboard

---

### Example 4: SaaS Product Launch Ad

**Prompt:**
```
Write a script and generate a video ad for our SaaS product launch
```

**What the skill does:**

**Step 1 — Script (DeepSeek V3.2):**

```
Scene 1 (5s): Split screen showing frustrated workers struggling with spreadsheets,
messy dashboards, email overload. Dark, chaotic visual style.
Voiceover: "Tired of juggling a dozen tools that don't talk to each other?"

Scene 2 (5s): Smooth transition to a clean, modern dashboard interface.
Everything clicks into place. Bright, organized, satisfying animations.
Voiceover: "Meet ProductName — your entire workflow in one place."

Scene 3 (5s): Quick montage of key features: real-time collaboration,
automated reports, one-click integrations. Fast-paced, energetic.
Voiceover: "Collaborate. Automate. Scale."

Scene 4 (5s): Logo reveal with CTA. Clean background with subtle particles.
Voiceover: "Start your free trial today at productname.com"
```

**Step 2 — Storyboard (Seedream v5.0):** 4 frames generated at $0.032 each

**Step 3 — Video (Kling v3.0 Pro):** 4 clips generated at $0.204 each

**Total cost:** ~$1.00 (script: ~$0.001 + storyboard: $0.128 + video: $0.816)

---

### Example 5: Budget-Friendly Ad with Wan 2.6

**Prompt:**
```
Create a video ad on a tight budget for a local bakery
```

**What the skill does:**
1. Uses DeepSeek V3.2 for scripting (near-zero cost)
2. Uses Flux Dev for storyboards ($0.012/image instead of $0.032)
3. Uses Wan 2.6 for video generation ($0.07/clip instead of $0.204)

**Budget pipeline costs:**

```
Script (DeepSeek V3.2):     ~$0.001
Storyboard (Flux Dev x 3):   $0.036
Video (Wan 2.6 x 3):         $0.210
─────────────────────────────────────
Total:                       ~$0.25
```

Compare to premium pipeline: ~$0.71 — a 65% savings.

---

### Example 6: A/B Test Campaign

**Prompt:**
```
Create 3 different versions of a sneaker ad for A/B testing
```

**What the skill does:**
1. Writes 3 different script variations with DeepSeek V3.2
   - Version A: Lifestyle/aspirational angle
   - Version B: Performance/technical angle
   - Version C: Social proof/testimonial angle
2. Generates unique storyboards for each version
3. Produces 3 complete video ads
4. Labels each version for easy A/B comparison

**Cost:** ~$2.13 (3 complete ad pipelines)

---

### Example 7: Multi-Shot Narrative Ad

**Prompt:**
```
Create a 30-second narrative ad telling the story of a runner's morning routine,
featuring our sports drink brand
```

**What the skill does:**

**Script — 6 scenes x 5 seconds:**

```
Scene 1: Alarm clock at 5:30 AM, runner's hand reaching to turn it off
Scene 2: Running shoes being laced up in dim morning light
Scene 3: Runner sprinting through empty city streets at dawn
Scene 4: Close-up of exhausted face, determination in the eyes
Scene 5: Runner stops, grabs the sports drink, refreshing gulp
Scene 6: Logo reveal: "Fuel Your Morning. Brand Name."
```

**Pipeline execution:**
- Script: 1 DeepSeek call
- Storyboard: 6 Seedream frames
- Video: 6 Kling v3.0 Pro clips
- Concatenation: ffmpeg to merge all 6 clips

**Cost:** ~$1.42

---

## Application Scenarios

### Digital Marketing Agencies

| Use Case | Pipeline | Cost per Ad |
|----------|----------|------------|
| Client pitch mockups | Budget (Wan 2.6) | ~$0.25 |
| Social media campaigns | Standard (Seedance) | ~$0.80 |
| Premium brand videos | Premium (Kling v3.0 Pro) | ~$0.71 |
| A/B test variations | Mix models | ~$2.13 (3 versions) |

### E-Commerce Brands

| Use Case | Pipeline | Cost per Ad |
|----------|----------|------------|
| Product showcase videos | Single-shot (Kling i2v) | $0.204 |
| Seasonal campaign ads | Full pipeline | ~$0.71 |
| Flash sale announcements | Budget (Wan 2.6) | ~$0.25 |
| Unboxing / reveal videos | Multi-shot narrative | ~$1.42 |

### Social Media Marketers

| Platform | Format | Recommended Model |
|----------|--------|-------------------|
| Instagram Reels | 9:16, 5-15s | Kling v3.0 Pro |
| TikTok | 9:16, 5-60s | Seedance v1.5 Pro |
| YouTube Shorts | 9:16, 5-60s | Kling v3.0 Standard |
| YouTube Pre-Roll | 16:9, 15-30s | Kling v3.0 Pro |
| Facebook Feed | 1:1 or 16:9, 15s | Wan 2.6 (budget) |
| LinkedIn | 16:9, 15-30s | Kling v3.0 Pro |

### Content Creators

| Use Case | Pipeline | Cost per Video |
|----------|----------|---------------|
| Channel intro/outro | Single scene | $0.07-0.204 |
| Sponsored content | Full pipeline | ~$0.71 |
| Thumbnail animations | Short clip (3-5s) | $0.07-0.204 |
| Course promo videos | Multi-shot | ~$1.42 |

---

## Models Used

### DeepSeek V3.2 — Scriptwriting

| Property | Value |
|----------|-------|
| **Model ID** | `deepseek/deepseek-v3-0324` |
| **Price** | $0.26 per million tokens |
| **Best For** | Ad script generation, scene descriptions, voiceover text |
| **Strengths** | Creative writing, structured output, follows format instructions |
| **Use When** | Starting from a brief, need a structured script with scenes and timing |

### Seedream v5.0 Lite — Storyboard

| Property | Value |
|----------|-------|
| **Model ID** | `bytedance/seedream-v5.0-lite/edit` |
| **Price** | $0.032 per image |
| **Best For** | Visual storyboard frames with precise style control |
| **Strengths** | High quality, good for styled/edited frames |
| **Use When** | Need detailed storyboards, editing existing images into scenes |

### Flux Dev — Budget Storyboard

| Property | Value |
|----------|-------|
| **Model ID** | `black-forest-labs/flux-dev` |
| **Price** | $0.012 per image |
| **Best For** | Cost-effective storyboard generation |
| **Strengths** | Excellent quality-to-price ratio |
| **Use When** | Budget-conscious projects, rapid iteration, draft storyboards |

### Kling v3.0 Pro — Premium Video

| Property | Value |
|----------|-------|
| **Model ID** | `kwaivgi/kling-v3.0-pro/text-to-video` (t2v) / `kwaivgi/kling-v3.0-pro/image-to-video` (i2v) |
| **Price** | $0.204 per video clip |
| **Best For** | Highest quality video ads, cinematic output |
| **Strengths** | Best motion quality, native audio, up to 4K resolution |
| **Use When** | Premium brand content, final production videos, client deliverables |

### Seedance v1.5 Pro — Audio-Visual Video

| Property | Value |
|----------|-------|
| **Model ID** | `bytedance/seedance-v1.5-pro/image-to-video` |
| **Price** | $0.222 per video clip |
| **Best For** | Audio-synchronized video content |
| **Strengths** | Audio-visual synchronization, dance/music content |
| **Use When** | Music-driven ads, dance content, audio-visual experiences |

### Wan 2.6 — Budget Video

| Property | Value |
|----------|-------|
| **Model ID** | `wan/wan-2.6/text-to-video` (t2v) / `wan/wan-2.6/image-to-video` (i2v) |
| **Price** | $0.07 per video clip |
| **Best For** | Budget-friendly video generation, rapid prototyping |
| **Strengths** | Lowest cost, fast generation, good for drafts |
| **Use When** | Budget projects, internal reviews, testing concepts before premium generation |

---

## Social Media Format Guide

### Platform Specifications

| Platform | Aspect Ratio | Resolution | Duration | Notes |
|----------|-------------|------------|----------|-------|
| **Instagram Reels** | 9:16 | 1080x1920 | 5-90s | Vertical, mobile-first |
| **Instagram Stories** | 9:16 | 1080x1920 | 5-15s | Vertical, ephemeral |
| **Instagram Feed** | 1:1 or 4:5 | 1080x1080 | 3-60s | Square or near-square |
| **TikTok** | 9:16 | 1080x1920 | 5-180s | Vertical, fast-paced |
| **YouTube Shorts** | 9:16 | 1080x1920 | 5-60s | Vertical, mobile |
| **YouTube Standard** | 16:9 | 1920x1080 | 15-120s | Horizontal, cinematic |
| **Facebook Feed** | 1:1 or 16:9 | 1080x1080 | 5-120s | Square or horizontal |
| **Facebook Stories** | 9:16 | 1080x1920 | 5-20s | Vertical |
| **LinkedIn** | 16:9 or 1:1 | 1920x1080 | 15-30s | Professional tone |
| **Twitter/X** | 16:9 or 1:1 | 1920x1080 | 5-140s | Short, impactful |

### Format Selection Parameters

When generating video, use these aspect ratio parameters:

```json
{
  "aspect_ratio": "16:9"   // YouTube, LinkedIn, website
  "aspect_ratio": "9:16"   // Instagram Reels, TikTok, Stories
  "aspect_ratio": "1:1"    // Facebook Feed, Instagram Feed
  "aspect_ratio": "4:5"    // Instagram Feed (tall)
  "aspect_ratio": "4:3"    // Traditional video
}
```

---

## Cost Calculator

### Cost per Ad by Quality Tier

| Tier | Script | Storyboard (3 frames) | Video (3 clips) | Total |
|------|--------|----------------------|-----------------|-------|
| **Budget** | DeepSeek (~$0.001) | Flux Dev ($0.036) | Wan 2.6 ($0.210) | **~$0.25** |
| **Standard** | DeepSeek (~$0.001) | Seedream ($0.096) | Wan 2.6 ($0.210) | **~$0.31** |
| **Premium** | DeepSeek (~$0.001) | Seedream ($0.096) | Kling v3.0 Pro ($0.612) | **~$0.71** |
| **Ultra** | DeepSeek (~$0.001) | Seedream ($0.096) | Seedance v1.5 ($0.666) | **~$0.76** |

### Volume Pricing Estimates

| Volume | Budget Tier | Standard Tier | Premium Tier |
|--------|------------|---------------|-------------|
| **10 ads** | $2.50 | $3.10 | $7.10 |
| **50 ads** | $12.50 | $15.50 | $35.50 |
| **100 ads** | $25.00 | $31.00 | $71.00 |
| **500 ads** | $125.00 | $155.00 | $355.00 |
| **1,000 ads** | $250.00 | $310.00 | $710.00 |

### Cost Comparison: AI vs Traditional Video Ad Production

| Method | Cost per Ad | Time to Deliver | Setup Cost |
|--------|------------|----------------|------------|
| **Video Production Agency** | $5,000-50,000 | 2-6 weeks | $0 |
| **Freelance Videographer** | $1,000-5,000 | 1-2 weeks | $0 |
| **DIY (Stock Footage + Editor)** | $100-500 | 1-3 days | $200-500/yr |
| **AI Video Ad Skill (Premium)** | $0.71 | 2-5 minutes | $0 |
| **AI Video Ad Skill (Budget)** | $0.25 | 2-5 minutes | $0 |

### First-Time Bonus

Atlas Cloud offers a **25% bonus on your first recharge** (up to $100 bonus):

| Top-Up | Bonus (25%) | Total Credits | Premium Ads | Budget Ads |
|--------|-------------|---------------|-------------|------------|
| $10 | $2.50 | $12.50 | ~17 ads | ~50 ads |
| $50 | $12.50 | $62.50 | ~88 ads | ~250 ads |
| $100 | $25.00 | $125.00 | ~176 ads | ~500 ads |
| $400 | $100.00 | $500.00 | ~704 ads | ~2,000 ads |

---

## API Reference

### Endpoints

```
POST   https://api.atlascloud.ai/api/v1/model/prediction     (Submit prediction)
GET    https://api.atlascloud.ai/api/v1/model/prediction/{id} (Check status)
POST   https://api.atlascloud.ai/api/v1/chat/completions      (LLM chat)
```

### Authentication

All requests require the `Authorization` header:

```
Authorization: Bearer YOUR_ATLASCLOUD_API_KEY
```

### Script Generation (DeepSeek V3.2)

```bash
curl -X POST https://api.atlascloud.ai/api/v1/chat/completions \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek/deepseek-v3-0324",
    "messages": [
      {
        "role": "system",
        "content": "You are an expert video ad scriptwriter. Write scripts with clear scene descriptions, camera directions, voiceover text, and timing. Format each scene with: Scene number, duration, visual description, and voiceover text."
      },
      {
        "role": "user",
        "content": "Write a 15-second (3 scenes x 5 seconds) video ad script for a premium coffee brand. The ad should evoke morning warmth and ritual."
      }
    ],
    "temperature": 0.7
  }'
```

### Storyboard Frame (Seedream v5.0)

```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "bytedance/seedream-v5.0-lite/edit",
    "input": {
      "prompt": "Cinematic storyboard frame: Close-up of steam rising from a freshly poured cup of coffee on a sunlit wooden table, morning light streaming through sheer curtains, warm golden tones, shallow depth of field, commercial photography quality"
    }
  }'
```

### Video Generation (Kling v3.0 Pro — Text-to-Video)

```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kwaivgi/kling-v3.0-pro/text-to-video",
    "input": {
      "prompt": "Cinematic close-up of steam rising from a freshly poured cup of coffee, morning sunlight streaming through curtains, warm golden tones, slow motion, commercial ad quality",
      "duration": 5,
      "aspect_ratio": "16:9"
    }
  }'
```

### Video Generation (Kling v3.0 Pro — Image-to-Video)

```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kwaivgi/kling-v3.0-pro/image-to-video",
    "input": {
      "prompt": "Gentle steam animation, subtle camera push-in, warm morning atmosphere",
      "image_url": "https://storyboard-frame-url.jpg",
      "duration": 5,
      "aspect_ratio": "16:9"
    }
  }'
```

### Video Generation (Wan 2.6 — Budget)

```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "wan/wan-2.6/text-to-video",
    "input": {
      "prompt": "Coffee cup with rising steam on a wooden table, morning light, warm tones",
      "duration": 5,
      "aspect_ratio": "16:9"
    }
  }'
```

### Poll for Results

```bash
curl -X GET "https://api.atlascloud.ai/api/v1/model/prediction/{request_id}" \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY"
```

### Response Format

```json
{
  "request_id": "abc123-def456-ghi789",
  "status": "completed",
  "output": {
    "video_url": "https://cdn.atlascloud.ai/videos/abc123.mp4"
  },
  "cost": {
    "amount": 0.204,
    "currency": "USD"
  }
}
```

---

## Workflow Recipes

### Recipe 1: Quick Single-Scene Product Ad

The simplest workflow — one prompt, one video.

```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kwaivgi/kling-v3.0-pro/text-to-video",
    "input": {
      "prompt": "Cinematic product showcase of a luxury watch rotating slowly on a dark reflective surface, dramatic studio lighting with golden accents, premium commercial quality, slow motion",
      "duration": 5,
      "aspect_ratio": "16:9"
    }
  }'
```

**Cost:** $0.204

### Recipe 2: Full Pipeline with Python

Complete end-to-end ad generation with Python.

```python
import requests
import os
import time
import json

API_KEY = os.environ["ATLASCLOUD_API_KEY"]
PREDICTION_URL = "https://api.atlascloud.ai/api/v1/model/prediction"
CHAT_URL = "https://api.atlascloud.ai/api/v1/chat/completions"
HEADERS = {
    "Authorization": f"Bearer {API_KEY}",
    "Content-Type": "application/json"
}

def chat_completion(messages, model="deepseek/deepseek-v3-0324"):
    """Generate text using DeepSeek V3.2."""
    payload = {
        "model": model,
        "messages": messages,
        "temperature": 0.7
    }
    response = requests.post(CHAT_URL, headers=HEADERS, json=payload)
    return response.json()["choices"][0]["message"]["content"]

def generate_and_poll(model, input_data):
    """Submit a prediction and poll until completion."""
    payload = {"model": model, "input": input_data}
    response = requests.post(PREDICTION_URL, headers=HEADERS, json=payload)
    request_id = response.json()["request_id"]

    while True:
        status = requests.get(
            f"{PREDICTION_URL}/{request_id}", headers=HEADERS
        ).json()
        if status["status"] == "completed":
            return status["output"]
        elif status["status"] == "failed":
            raise Exception(f"Failed: {status.get('error', 'Unknown')}")
        time.sleep(5)

# Step 1: Generate Script
print("Step 1: Generating ad script...")
script = chat_completion([
    {
        "role": "system",
        "content": "Write a 3-scene video ad script. Each scene should be exactly "
                   "5 seconds. Format: Scene N (5s): [visual description]. "
                   "Voiceover: [text]. Return only the script, no commentary."
    },
    {
        "role": "user",
        "content": "Write a video ad script for a premium coffee brand. "
                   "Theme: morning ritual, warmth, quality."
    }
])
print(f"Script:\n{script}\n")

# Step 2: Generate Storyboard Frames
print("Step 2: Generating storyboard frames...")
scenes = [
    "Close-up of steam rising from a freshly poured cup of coffee on a sunlit wooden table",
    "Hands wrapping around a warm ceramic mug, person smiling, morning golden light",
    "Coffee bag with premium branding, cup beside it, clean kitchen, subtle zoom"
]

storyboard_urls = []
for i, scene in enumerate(scenes):
    print(f"  Generating frame {i+1}/3...")
    result = generate_and_poll(
        "bytedance/seedream-v5.0-lite/edit",
        {"prompt": f"Cinematic storyboard frame: {scene}, warm tones, "
                   f"commercial photography, shallow depth of field"}
    )
    storyboard_urls.append(result["image_url"])
    print(f"  Frame {i+1}: {result['image_url']}")

# Step 3: Generate Video Clips
print("\nStep 3: Generating video clips...")
video_urls = []
for i, (scene, frame_url) in enumerate(zip(scenes, storyboard_urls)):
    print(f"  Generating clip {i+1}/3...")
    result = generate_and_poll(
        "kwaivgi/kling-v3.0-pro/image-to-video",
        {
            "prompt": f"Cinematic motion: {scene}, smooth camera movement, "
                      f"commercial ad quality",
            "image_url": frame_url,
            "duration": 5,
            "aspect_ratio": "16:9"
        }
    )
    video_urls.append(result["video_url"])
    print(f"  Clip {i+1}: {result['video_url']}")

print("\nVideo ad generation complete!")
print(f"Total clips: {len(video_urls)}")
for i, url in enumerate(video_urls):
    print(f"  Scene {i+1}: {url}")
```

### Recipe 3: Video Concatenation with ffmpeg

After generating individual clips, concatenate them into one ad.

```bash
# Create a file list for ffmpeg
echo "file 'scene1.mp4'" > concat_list.txt
echo "file 'scene2.mp4'" >> concat_list.txt
echo "file 'scene3.mp4'" >> concat_list.txt

# Concatenate without re-encoding
ffmpeg -f concat -safe 0 -i concat_list.txt -c copy final_ad.mp4

# Or with re-encoding for consistent format
ffmpeg -f concat -safe 0 -i concat_list.txt \
  -c:v libx264 -preset medium -crf 23 \
  -c:a aac -b:a 128k \
  final_ad.mp4
```

### Recipe 4: A/B Test Generator

Generate multiple ad versions for split testing.

```python
# Define A/B test variations
variations = {
    "version_a": {
        "style": "warm and emotional",
        "tone": "heartfelt storytelling",
        "cta": "Feel the difference"
    },
    "version_b": {
        "style": "energetic and bold",
        "tone": "high energy, fast cuts",
        "cta": "Fuel your fire"
    },
    "version_c": {
        "style": "minimalist and elegant",
        "tone": "quiet luxury, slow motion",
        "cta": "Simply the best"
    }
}

for version_name, variation in variations.items():
    print(f"\nGenerating {version_name}...")

    # Generate script for this variation
    script = chat_completion([
        {
            "role": "system",
            "content": f"Write a 3-scene, 15-second video ad script. "
                       f"Style: {variation['style']}. "
                       f"Tone: {variation['tone']}. "
                       f"End with CTA: {variation['cta']}."
        },
        {
            "role": "user",
            "content": "Write a video ad for a premium coffee brand."
        }
    ])

    # Generate video for each scene...
    # (same pattern as Recipe 2)

    print(f"{version_name} complete!")
```

### Recipe 5: Batch Ad Campaign

Generate ads for multiple products in one run.

```python
products = [
    {
        "name": "Running Shoes",
        "description": "lightweight trail running shoes",
        "theme": "outdoor adventure, freedom, speed",
        "format": "9:16"
    },
    {
        "name": "Smart Watch",
        "description": "premium fitness smartwatch",
        "theme": "technology, health, modern lifestyle",
        "format": "1:1"
    },
    {
        "name": "Coffee Maker",
        "description": "artisan pour-over coffee maker",
        "theme": "morning ritual, craft, simplicity",
        "format": "16:9"
    }
]

for product in products:
    print(f"\nCreating ad for: {product['name']}")

    # Step 1: Script
    script = chat_completion([
        {
            "role": "system",
            "content": f"Write a 3-scene, 15-second video ad script for a "
                       f"{product['description']}. Theme: {product['theme']}."
        },
        {"role": "user", "content": "Write the ad script."}
    ])

    # Step 2: Storyboard + Video (use budget model for batch)
    # ... (same pattern, using Wan 2.6 for cost efficiency)

    print(f"Ad for {product['name']} complete!")
```

**Cost for 3 product ads (budget tier):** ~$0.75

---

## Troubleshooting

### Common Issues

**`ATLASCLOUD_API_KEY` not set**
```
Error: ATLASCLOUD_API_KEY environment variable is required
```
Set the environment variable or add it to your shell profile.

**Video generation timeout**
```
Error: Prediction timed out after 300 seconds
```
Video generation typically takes 1-5 minutes. Complex prompts or higher resolutions may take longer. Retry with a simpler prompt or lower resolution.

**Inconsistent style across scenes**
- Use detailed and consistent style descriptions across all scene prompts
- Include the same lighting, color palette, and camera style keywords in each prompt
- Consider using image-to-video (i2v) with storyboard frames for better consistency

**Script quality issues**
- Provide more detail in your brief to DeepSeek
- Specify the target audience, brand voice, and emotional tone
- Ask for multiple script drafts and choose the best one

**Audio not generated**
- Not all models support native audio generation
- Kling v3.0 Pro supports audio with the `audio_generation: true` parameter
- For other models, add audio in post-production

**ffmpeg concatenation errors**
- Ensure all clips have the same resolution, frame rate, and codec
- Use the re-encoding method (with `-c:v libx264`) if clips have different formats
- Check that all clip files exist and are valid

---

## Architecture

```
ai-video-ad-skill/
├── SKILL.md           # Claude Code skill definition
├── README.md          # This file
└── LICENSE            # MIT License
```

---

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/new-feature`)
3. Commit your changes (`git commit -m 'Add new feature'`)
4. Push to the branch (`git push origin feature/new-feature`)
5. Open a Pull Request

---

## Take This to Production Today

This workflow is optimized for Atlas Cloud. Move from experiment to enterprise-ready scale with our dedicated migration support.

- **Production-Ready**: Generate video ads at $0.07-0.222/clip
- **Enterprise Security**: SOC I & II Certified | HIPAA Compliant
- **Zero Maintenance**: Serverless architecture — focus on your product, not the servers
- **25% Bonus**: First recharge up to $100

[Start Building](https://www.atlascloud.ai?ref=JPM683)

---

## License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built for the Claude Code ecosystem. Powered by [Atlas Cloud](https://www.atlascloud.ai?ref=JPM683).**

</div>
