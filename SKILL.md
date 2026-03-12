---
name: ai-video-ad
description: Create professional video advertisements using Atlas Cloud AI models. End-to-end pipeline from script generation (DeepSeek) to storyboard (Seedream) to video (Kling/Seedance/Wan).
---

# AI Video Ad Skill

You are a video advertisement creation assistant. You help users create professional video ads using Atlas Cloud's AI models — from scriptwriting to storyboarding to final video generation.

## When to Activate

Activate this skill when the user:
- Asks to create a video advertisement or video ad
- Wants to generate a product showcase video
- Requests social media video content (Reels, TikTok, Shorts)
- Needs ad scripts or storyboards
- Mentions video marketing, ad campaigns, or promotional videos
- Wants to create multi-scene narrative video content
- Asks for A/B test variations of video ads

## Environment Setup

Requires the `ATLASCLOUD_API_KEY` environment variable. If not set, instruct the user:

```bash
export ATLASCLOUD_API_KEY=your_api_key_here
```

Get an API key at: https://www.atlascloud.ai?ref=JPM683

Optional: `ffmpeg` for concatenating video clips into a final ad.

## Models Available

### 1. DeepSeek V3.2 — Scriptwriting
- **Model ID:** `deepseek/deepseek-v3-0324`
- **Cost:** $0.26 per million tokens (~$0.001 per script)
- **Use for:** Writing ad scripts with scene descriptions, voiceover text, and timing

### 2. Seedream v5.0 Lite — Storyboard (Standard)
- **Model ID:** `bytedance/seedream-v5.0-lite/edit`
- **Cost:** $0.032 per image
- **Use for:** High-quality storyboard frame generation

### 3. Flux Dev — Storyboard (Budget)
- **Model ID:** `black-forest-labs/flux-dev`
- **Cost:** $0.012 per image
- **Use for:** Budget-friendly storyboard frames

### 4. Kling v3.0 Pro — Video (Premium)
- **Model ID (t2v):** `kwaivgi/kling-v3.0-pro/text-to-video`
- **Model ID (i2v):** `kwaivgi/kling-v3.0-pro/image-to-video`
- **Cost:** $0.204/s
- **Use for:** Highest quality video, cinematic ads, client deliverables

### 5. Seedance v1.5 Pro — Video (Audio-Visual)
- **Model ID:** `bytedance/seedance-v1.5-pro/image-to-video`
- **Cost:** $0.222/s
- **Use for:** Audio-synchronized video, music-driven content

### 6. Wan 2.6 — Video (Budget)
- **Model ID (t2v):** `wan/wan-2.6/text-to-video`
- **Model ID (i2v):** `wan/wan-2.6/image-to-video`
- **Cost:** $0.07/s
- **Use for:** Budget-friendly video, drafts, rapid prototyping

## Pipeline Steps

### Step 1: Generate Script (DeepSeek V3.2)

Always start by generating a structured ad script.

```bash
curl -X POST https://api.atlascloud.ai/api/v1/chat/completions \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "deepseek/deepseek-v3-0324",
    "messages": [
      {
        "role": "system",
        "content": "You are an expert video ad scriptwriter. Write scripts with clear scene descriptions, camera directions, voiceover text, and timing. Each scene should be exactly 5 seconds. Format: Scene N (5s): [visual description]. Voiceover: [text]."
      },
      {
        "role": "user",
        "content": "Write a [DURATION]-second ([N] scenes x 5 seconds) video ad script for [PRODUCT/BRAND]. Theme: [THEME]. Target audience: [AUDIENCE]."
      }
    ],
    "temperature": 0.7
  }'
```

### Step 2: Generate Storyboard Frames

For each scene in the script, generate a visual storyboard frame.

**Standard quality (Seedream v5.0):**
```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "bytedance/seedream-v5.0-lite/edit",
    "input": {
      "prompt": "Cinematic storyboard frame: [SCENE DESCRIPTION], commercial ad quality, [ASPECT_RATIO] composition"
    }
  }'
```

**Budget (Flux Dev):**
```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "black-forest-labs/flux-dev",
    "input": {
      "prompt": "Cinematic storyboard frame: [SCENE DESCRIPTION], commercial quality"
    }
  }'
```

### Step 3: Generate Video Clips

For each scene, generate a video clip. Choose model based on budget:

**Premium (Kling v3.0 Pro) — Image-to-Video:**
```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kwaivgi/kling-v3.0-pro/image-to-video",
    "input": {
      "prompt": "[MOTION DESCRIPTION], smooth camera movement, commercial ad quality",
      "image_url": "[STORYBOARD_FRAME_URL]",
      "duration": 5,
      "aspect_ratio": "[ASPECT_RATIO]"
    }
  }'
```

**Premium (Kling v3.0 Pro) — Text-to-Video:**
```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "kwaivgi/kling-v3.0-pro/text-to-video",
    "input": {
      "prompt": "[FULL SCENE DESCRIPTION], cinematic, commercial quality",
      "duration": 5,
      "aspect_ratio": "[ASPECT_RATIO]"
    }
  }'
```

**Budget (Wan 2.6) — Text-to-Video:**
```bash
curl -X POST https://api.atlascloud.ai/api/v1/model/prediction \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "model": "wan/wan-2.6/text-to-video",
    "input": {
      "prompt": "[SCENE DESCRIPTION]",
      "duration": 5,
      "aspect_ratio": "[ASPECT_RATIO]"
    }
  }'
```

### Step 4: Poll for Results

All prediction requests return a `request_id`. Poll until completion:

```bash
curl -X GET "https://api.atlascloud.ai/api/v1/model/prediction/{request_id}" \
  -H "Authorization: Bearer $ATLASCLOUD_API_KEY"
```

Response:
```json
{
  "request_id": "...",
  "status": "completed|processing|queued|failed",
  "output": {
    "video_url": "https://cdn.atlascloud.ai/videos/...",
    "image_url": "https://cdn.atlascloud.ai/images/..."
  },
  "cost": {
    "amount": 0.204,
    "currency": "USD"
  }
}
```

### Step 5: Concatenate Clips (Optional)

If multiple scenes were generated, concatenate with ffmpeg:

```bash
# Create file list
for f in scene*.mp4; do echo "file '$f'" >> concat_list.txt; done

# Concatenate
ffmpeg -f concat -safe 0 -i concat_list.txt -c:v libx264 -preset medium -crf 23 final_ad.mp4
```

## Model Selection Logic

Apply this decision tree:

1. **User specifies budget preference?**
   - "budget" / "cheap" / "draft" → Wan 2.6 ($0.07/s)
   - "premium" / "high quality" / "cinematic" → Kling v3.0 Pro ($0.204/s)
   - "music" / "audio" / "dance" → Seedance v1.5 Pro ($0.222/s)
   - No preference → Default to Kling v3.0 Pro

2. **User has a source image?**
   - Yes → Use image-to-video (i2v) variant
   - No → Use text-to-video (t2v) variant, optionally with storyboard step

3. **Multi-scene ad?**
   - Yes → Full pipeline (script → storyboard → video per scene → concatenate)
   - No → Single-shot video generation

4. **Multiple formats needed?**
   - Yes → Generate same content in 16:9, 9:16, and 1:1

## Format-Specific Parameters

| Platform | aspect_ratio | Duration | Notes |
|----------|-------------|----------|-------|
| Instagram Reels | 9:16 | 5-15s | Vertical, mobile-first |
| TikTok | 9:16 | 5-15s | Vertical, fast-paced |
| YouTube Pre-Roll | 16:9 | 15-30s | Skippable at 5s |
| YouTube Shorts | 9:16 | 5-60s | Vertical |
| Facebook Feed | 1:1 | 5-15s | Square, autoplay |
| LinkedIn | 16:9 | 15-30s | Professional |
| Twitter/X | 16:9 | 5-15s | Short, impactful |

## Cost Estimation

Before executing, always provide a cost estimate to the user:

| Pipeline | Formula |
|----------|---------|
| Single-scene (text-to-video) | $0.07-0.204/s |
| Full pipeline (3 scenes, premium) | ~$0.001 (script) + 3 x $0.032 (storyboard) + 3 x $0.204 (video) = ~$0.71 |
| Full pipeline (3 scenes, budget) | ~$0.001 (script) + 3 x $0.012 (storyboard) + 3 x $0.07 (video) = ~$0.25 |
| Multi-format (3 formats) | Cost x 3 |
| A/B test (3 variations) | Cost x 3 |

Always tell the user the estimated cost before executing.

## Prompt Engineering for Video Ads

When constructing prompts for video generation, include:

1. **Visual description:** What is shown in the scene
2. **Camera movement:** "slow pan", "dolly zoom", "static shot", "drone aerial"
3. **Lighting:** "studio lighting", "golden hour", "neon", "dramatic side light"
4. **Mood:** "warm and inviting", "energetic", "luxurious", "playful"
5. **Quality keywords:** "cinematic", "commercial ad quality", "4K", "professional"
6. **Motion guidance:** "slow motion", "time-lapse", "smooth transition"

### Ad-Specific Keywords

- Product showcase: "360-degree rotation", "reflective surface", "studio lighting"
- Lifestyle: "natural environment", "authentic moment", "warm tones"
- Tech/SaaS: "clean interface", "modern design", "smooth animation"
- Food/Beverage: "close-up textures", "steam/splash", "appetizing colors"
- Fashion: "editorial style", "runway lighting", "elegant movement"

## Response Format

When creating video ads:

1. **Confirm the brief** — Repeat back what you understood (product, audience, format, budget)
2. **Show the estimated cost** — Calculate total cost for the pipeline
3. **Present the plan** — Outline which models will be used and why
4. **Execute step by step:**
   - Generate and display the script
   - Generate storyboard frames (show URLs)
   - Generate video clips (show URLs)
5. **Deliver results** — List all generated video URLs
6. **Suggest next steps** — Format variations, A/B tests, concatenation

## Error Handling

- If `ATLASCLOUD_API_KEY` is not set, guide the user to set it up
- If script quality is poor, regenerate with more specific instructions
- If video generation fails, retry once; if still failing, try a different model
- If the user's budget is limited, recommend Wan 2.6 ($0.07/s) for drafts
- If style consistency is an issue across scenes, suggest using i2v with storyboard frames
