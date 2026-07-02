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
- Calculates output size from the original width and height before enhancing
- Improves clarity, edge sharpness, and text readability
- Reduces blur, compression artifacts, jagged edges, noise, and mosaic-like blockiness
- Keeps composition, subjects, expressions, UI layout, text content, color mood, and visual style faithful to the source
- Handles long posters, portfolio pages, UI long screenshots, and infographics by prioritizing readable width/short side rather than only longest-side 4K
- Detects when the source image is too blurry to faithfully recover small text and asks for a better original instead of inventing content
- Outputs cleaner high-resolution PNG images suitable for social media, PPT, documentation, and publishing

## What It Avoids

- Redesigning the image
- Changing composition or layout
- Swapping portrait and landscape orientation
- Cropping, padding, stretching, or forcing images into 1:1, 16:9, 4:3, or platform ratios
- Replacing or rewriting text
- Inventing unreadable text, contact details, dates, links, names, or portfolio content
- Adding or removing elements
- Changing identity features, expressions, poses, or UI structure
- Turning photos into illustrations or illustrations into photos
- Over-polishing memes until they lose their original humor

## Size Rules

The skill must read the source width and height first. Output dimensions should always be calculated from the original size using one uniform scale factor.

- `2x`, `3x`, `4x`: multiply both width and height by that factor
- `4K` for normal photos or memes: scale the longest side to 3840px by default and calculate the other side proportionally
- `4K` for long images, portfolio pages, UI long screenshots, and text-heavy infographics: do not stop at longest-side 3840px, because the readable side may remain too small. Prefer at least `2x`, or set the width/short side high enough for text readability.
- `short side 4K`: only then scale the shortest side to 3840px
- Explicit width and height: use only if they preserve the original aspect ratio

Example: a `1239x1332` portrait image should become `4956x5328` at `4x`, or about `3572x3840` for longest-side 4K. It should not become landscape or `3840x2160`.

For long images, a `750x5000` source should not become `576x3840`, because the width gets smaller and text will not become clearer. Use at least `1500x10000`, or `2250x15000` / `3000x20000` when small text needs to be readable.

## Source Quality Limits

For text-heavy portfolio pages, resumes, UI long screenshots, posters, and infographics, the skill should not pretend that unreadable source text can be faithfully recovered by generation. If small text is already smeared into blocks or broken strokes, ask for a better source such as:

- Original PNG/JPG export
- PDF
- Figma, Sketch, PSD, AI, PPT, or another design source
- Original webpage, HTML, or page link
- Higher-resolution uncompressed screenshot

If the user chooses to continue with only the low-resolution image, the result should be described as faithful cleanup of visible information only. Rebuilding the text via OCR and layout recreation is a separate reconstruction workflow, not faithful 1:1 upscaling.

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
