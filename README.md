# Faithful Image Upscaler

A Codex skill for faithful image upscaling, clarity enhancement, and 1:1 visual restoration.

This skill is designed for images where preservation matters: memes, avatars, posters, covers, UI screenshots, product images, old photos, compressed images, and images with text. Its core rule is simple: keep the original image content, composition, proportions, text, subject, expression, and style unchanged while improving resolution, sharpness, detail, and readability.

## Skill

This repository contains the Codex skill:

```text
faithful-image-upscaler
```

The main skill definition is in [`SKILL.md`](./SKILL.md).

## What It Does

- Upscales images while preserving the original aspect ratio
- Improves clarity, edge sharpness, and text readability
- Reduces blur, compression artifacts, jagged edges, noise, and mosaic-like blockiness
- Keeps composition, subjects, expressions, UI layout, text content, color mood, and visual style faithful to the source
- Outputs cleaner high-resolution PNG images suitable for social media, PPT, documentation, and publishing

## What It Avoids

- Redesigning the image
- Changing composition or layout
- Replacing or rewriting text
- Adding or removing elements
- Changing identity features, expressions, poses, or UI structure
- Turning photos into illustrations or illustrations into photos
- Over-polishing memes until they lose their original humor

## Installation

Copy this repository's `faithful-image-upscaler` skill into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills/faithful-image-upscaler
cp SKILL.md ~/.codex/skills/faithful-image-upscaler/SKILL.md
```

Then restart Codex so it can pick up the new skill.

## Usage Examples

Use the skill in Codex with prompts like:

```text
Use faithful-image-upscaler to upscale this image to 4K while keeping it 1:1 faithful.
```

```text
高清放大这张图，保持原图内容和文字不变。
```

```text
高清放大并 1:1 还原，不要重新设计。
```

```text
Sharpen this blurry screenshot and improve text readability without changing the UI layout.
```

## Best For

- Memes and reaction images
- Avatars
- UI screenshots
- Posters and social covers
- Product images
- Old photos
- Compressed or low-resolution images
- Images with important text

## Notes

For tiny or heavily compressed source images, this skill should prefer faithful cleanup and controlled sharpening over generative redesign. It can make an image clearer and larger, but it should not invent new content or alter the visual memory of the original.
