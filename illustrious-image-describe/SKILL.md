---
name: illustrious-image-describe
description: Use when the user sends an image and wants it described as a paste-ready Illustrious (SDXL anime) prompt. Turns any picture into a faithful Danbooru-style tag prompt plus a short negative prompt.
---

# Illustrious Image Describe

Turn any image into one faithful, paste-ready Illustrious prompt that describes the picture for what it is. Illustrious is an SDXL anime model trained on Danbooru-style tags.

## When to use
- The user sends an image and asks you to describe it, recreate it, or turn it into an Illustrious prompt.
- The user describes a scene in words and wants it written as an Illustrious tag prompt.

## How to respond
- Reply with a single prompt inside one code block, ready to paste. Include a short negative prompt under a `Negative:` line in the same block.
- Describe what is actually in the image. Keep the subjects, clothing, pose, setting, colors, lighting and framing faithful to the source. Do not invent a different scene unless the user asks for changes.
- Ask a question only if the image cannot be read.
- Adult content follows the host platform's policies. Every person depicted must be an adult.

## Format
Write comma-separated Danbooru-style tags in a single line (or a few wrapped lines). Use lowercase tags. Spaces or underscores are both accepted; pick one and stay consistent. Do not write natural-language paragraphs as the main prompt.

Use this tag order:

1. **Quality and meta:** `masterpiece, best quality, amazing quality, very aesthetic, absurdres, newest`
2. **Rating,** only when it matches the image: `general`, `sensitive`, `nsfw`, or `explicit`
3. **Subject count:** `1girl`, `1boy`, `1other`, `2girls`, `solo`, `solo focus`, and so on
4. **Character and series,** if a known character is clearly intended: the character tag, then the series tag
5. **Appearance:** hair color, hair length and style, bangs, eye color, skin, distinctive features, makeup, jewelry
6. **Body and outfit:** build only when it is visible and useful, then every garment, its color, and how it is worn, plus shoes or barefoot
7. **Expression and pose:** smile, looking at viewer, sitting, standing, and the placement of arms, hands and legs
8. **Action and props:** what the subject is doing and any objects they hold
9. **Setting and background:** location, furniture, weather, time of day, background type
10. **Lighting and atmosphere:** sunlight, lamp light, rim light, chiaroscuro, and so on
11. **Composition and framing:** `cowboy shot`, `upper body`, `full body`, `close-up`, `from side`, `from above`, `from below`, `looking at viewer`, `profile`

If the image contains visible text, add a short tag or a brief quoted phrase for the exact words.

## Negative prompt
Keep the negative short. A reliable default is:

```
worst quality, low quality, lowres, bad anatomy, bad hands, extra digits, missing fingers, jpeg artifacts, signature, watermark, blurry
```

Add a term only when it would clearly fix a problem you can see or predict. Long kitchen-sink negatives often hurt Illustrious more than they help. Year tags such as `old` or `oldest` belong in the negative only when you want a modern look and the default already includes `newest` in the positive.

## Tips
- Prefer canonical Danbooru tag names (`long hair`, `school uniform`, `looking at viewer`) over invented phrases.
- Be specific. Name colors, garments and poses instead of vague adjectives.
- Give each person enough tags that the model can keep them distinct. For two or more people, use count tags and describe each person's hair, outfit and position.
- Do not pile on quality tags beyond the short set above. Extra fluff such as `8k` or `ultra detailed` adds little on Illustrious.
- Artist tags are optional. Add one only when the user asks for a particular look, and only if that artist tag is known to the checkpoint.
- Illustrious is an illustration model. If the source is a photograph, still write it as an anime or illustrated scene unless the user asks for a different medium.

## Example

Prompt for an illustration of a girl reading by a window:

```
masterpiece, best quality, amazing quality, very aesthetic, absurdres, newest, general, 1girl, solo, young adult, oval face, hazel eyes, long eyelashes, straight eyebrows, light freckles, closed mouth, slight smile, shoulder-length wavy chestnut hair, hair behind ear, gold hoop earrings, slim, oversized cream sweater, sleeves pushed up, charcoal leggings, gray wool socks, sitting, knees up, holding book, looking down, window seat, rainy window, sage green cushions, knitted throw, stack of books, potted plant, mug, indoor, overcast daylight, lamp light, cowboy shot, from side, three-quarter view

Negative: worst quality, low quality, lowres, bad anatomy, bad hands, extra digits, missing fingers, jpeg artifacts, signature, watermark, blurry
```
