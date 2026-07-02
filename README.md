# 4K Image Enhancer

A Codex skill for improving image quality, especially small screenshots, memes, and compressed images that need to be enlarged for clearer viewing or sharing.

The skill focuses on practical image enhancement workflows:

- Upscale low-resolution images toward 4K quality
- Improve sharpness and edge clarity
- Reduce visible compression artifacts and noise
- Preserve the original image content as much as possible
- Prepare screenshots and social images for publishing, documentation, or presentations

## Skill

This repository contains the Codex skill:

```text
4k-image-enhancer
```

The main skill definition is in [`SKILL.md`](./SKILL.md).

## Installation

Copy this repository's `4k-image-enhancer` skill into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills/4k-image-enhancer
cp SKILL.md ~/.codex/skills/4k-image-enhancer/SKILL.md
```

Then restart Codex so it can pick up the new skill.

## Usage Examples

Use the skill in Codex with prompts like:

```text
Use 4k-image-enhancer to upscale this image to 4K.
```

```text
Improve the image quality of screenshot.png.
```

```text
Sharpen this blurry screenshot and reduce compression artifacts.
```

```text
Enhance all PNG files in this folder.
```

## Best For

- Memes and reaction images
- UI screenshots
- Documentation screenshots
- Blog and newsletter images
- Social media images
- Presentation assets

## Notes

The skill is designed to preserve the original image rather than creatively redraw it. For very small or heavily compressed images, the output can be much larger and cleaner, but it cannot recover details that are not present in the source image unless a generative image workflow is used separately.
