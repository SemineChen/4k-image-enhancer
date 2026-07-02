# Universal Faithful Image Enhancer

A Codex skill for faithful image upscaling, clarity enhancement, detail recovery, and compression-artifact cleanup.

The skill keeps the original content, composition, aspect ratio, text, numbers, contact details, subjects, and visual style unchanged. It is for making the original image clearer and more publish-ready, not for redesigning or replacing it.

## Skill

```text
faithful-image-upscaler
```

The skill definition is in [`SKILL.md`](./SKILL.md).

## Core Workflow

- Read source width, height, aspect ratio, and content type before processing
- Detect long images, large images, UI screenshots, posters, resumes, portfolios, infographics, tables, and text-heavy images
- Choose whole-image enhancement for normal photos, avatars, products, posters, covers, and illustrations
- Use text-protected enhancement for UI, web, and app screenshots
- Use segmented enhancement plus seamless stitching for long images and text-heavy portfolio/resume/infographic images
- Apply local ROI enhancement to text cards, icons, illustrations, buttons, and user-marked regions inside each segment
- Validate size, content fidelity, clarity, and stitching before delivery

## Long Image Rules

Long and text-heavy images should not default to longest-side 3840px, because that can leave the readable width too small.

- Long images default to at least 2x
- Text-heavy long images prefer 3x
- Very dense small text can require 4x
- Minimum recommended width: 2160px
- Preferred width: 2400px to 3200px
- Dense text: 3200px or more

Examples:

- `818x2048`: prefer `2454x6144` or `3272x8192` for portfolio-style long images
- `750x5000`: do not output `576x3840`; prefer `2250x15000` or `3000x20000`
- `1200x6000`: prefer `2400x12000` or `3600x18000`

## Text Protection

For text-heavy images, the priority order is:

1. Do not change text
2. Do not change numbers
3. Do not change emails
4. Do not change links
5. Do not change headings
6. Do not change button copy
7. Do not move text
8. Preserve font style as much as possible
9. Only improve edge clarity and contrast

If the source text is already smeared into unreadable blocks, the skill should say that faithful 1:1 text recovery is not guaranteed. It may still enhance visible image quality, but truly clear text may require SVG, HTML, Figma, PDF, or another vector/source reconstruction workflow.

## Local ROI Enhancement

For long or text-heavy images, the skill should not stop after whole-segment upscaling. It must identify local regions of interest and enhance them separately:

- Text cards and paragraphs
- Dates, numbers, percentages, emails, phones, and links
- Icons, logos, buttons, labels, and badges
- Illustrations, product screenshots, UI components, and timeline blocks
- User-marked regions such as red boxes

Each ROI should be cropped, enhanced locally, and pasted back to the exact original coordinates. At 100% zoom, these ROI areas must be clearer than the source. If a marked ROI is still blurry, the result is not ready.

## Installation

```bash
mkdir -p ~/.codex/skills/faithful-image-upscaler
cp SKILL.md ~/.codex/skills/faithful-image-upscaler/SKILL.md
```

Restart Codex after installation.

## Example Prompts

```text
高清这张图
```

```text
高清放大这张长图，保持文字和布局不变。
```

```text
4K 修复，1:1 保留原图内容。
```

```text
Enhance this UI screenshot without changing text or layout.
```
