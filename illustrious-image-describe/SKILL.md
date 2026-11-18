---
name: illustrious-image-describe
description: Use when the user sends an image and wants it described as a paste-ready Illustrious (SDXL anime) prompt. Turns any picture into a faithful Danbooru-style tag prompt in the standard count, character, rating, general, artist, quality, year order, plus a compact negative prompt.
---

# Illustrious Image Describe

Turn any image into one faithful, paste-ready Illustrious prompt that describes the picture for what it is. Illustrious is a fine-tuned SDXL anime model trained on Danbooru tags (Danbooru2023-style data at 1024x1024). It is not Pony or NoobAI, and it does not use e621 or Pony score tags.

This skill follows the tag order, syntax, quality tags, negative prompt, and tips in [Illustrious Prompt Guide (Optimized & Complete)](https://civitai.com/articles/16016/illustrious-prompt-guide-optimized-and-complete), an optimized presentation of wolf999's guide.

## When to use
- The user sends an image and asks you to describe it, recreate it, or turn it into an Illustrious prompt.
- The user describes a scene in words and wants it written as an Illustrious tag prompt.

## How to respond
- Reply with a single prompt inside one code block, ready to paste. Include a short negative prompt under a `Negative:` line in the same block.
- Describe what is actually in the image. Keep the subjects, clothing, pose, setting, colors, lighting and framing faithful to the source. Do not invent a different scene unless the user asks for changes.
- Ask a question only if the image cannot be read.
- Adult content follows the host platform's policies. Every person depicted must be an adult.

## Format
Write comma-separated Danbooru-style tags. Tag order affects the output, so keep this sequence and do not rearrange the groups:

`person count, character name, rating, general tags, artist, score, year modifier`

Example of the skeleton:

```
1boy, kinoshita hideyoshi, general, building, itomugi-kun, masterpiece, newest
```

Character, rating, and artist are optional. The rest of the order should stay fixed.

Use this as the working order:

1. **Person count:** `1girl`, `1boy`, `1other`, `2girls`, and so on. `solo` may follow the count when there is only one subject.
2. **Character name,** if a known character is clearly intended, in Danbooru name order: `kinoshita hideyoshi`, not the reversed Western order. Then the series tag if it helps identity.
3. **Rating,** only when it is useful (see below). This slot is optional.
4. **General tags:** appearance, outfit, expression, pose, camera and composition, setting and background, lighting and effects, and medium or style if they are visible.
5. **Artist,** only when the user asks for one. Prefer artists with a large Danbooru presence (the guide suggests 100 or more posts).
6. **Score / quality:** `masterpiece`
7. **Year modifier:** `newest` (or `recent`, `mid`, `early`, `old` if that better matches the image's era)

If the image contains visible text, add a short general tag or a brief quoted phrase for the exact words.

### Rating tags
Danbooru's current ratings are:

- `general`: SFW for all ages
- `sensitive`: soft fanservice
- `questionable`: mildly NSFW
- `explicit`: NSFW / adult only

Rating is optional. Be careful with `general`: it was added late, and using it can filter out most of the training data. For an ordinary SFW scene, omit the rating tag unless the user asks for it. Use `sensitive`, `questionable`, or `explicit` when they clearly match the image.

### Quality and resolution tags
Place `masterpiece` and the year modifier at the end of the prompt, after the general tags and any artist tag.

Do not use Pony `score_9` or other non-Danbooru quality fluff such as `8k`, `4k`, `hdr`, `high quality`, or `detailed`. They are usually ineffective.

Do not use resolution tags (`lowres`, `highres`, `absurdres`, `incredibly absurdres`) in the positive prompt. The guide treats them as harmful or pointless.

### Tag syntax
- Write tags in lowercase: `masterpiece`, not `Masterpiece`.
- Commas are required. The model was trained on comma-separated tags. Write `sleeveless, striped shirt, collared shirt`, not `sleeveless striped collared shirt`.
- Spaces and underscores both work (`open mouth` or `open_mouth`), except in rare exact tags such as `+_+`.
- If a tag contains a smiley or similar symbol, escape it in A1111-style interfaces: `\:p`, `\:)`.
- Prefer canonical Danbooru tags. Look up unfamiliar tags on the [Danbooru Wiki](https://danbooru.donmai.us/wiki_pages/help:home). Tags with fewer than about 100 images often will not hold.

### Token budget
SDXL's main text encoder handles about 75 tokens. Longer prompts are split and can lose quality. Keep the tag list focused. Prioritize count, identity, defining appearance, pose, camera and setting, then `masterpiece, newest`. For a very complex scene, note that inpainting with a short regional prompt can be more reliable than one oversized prompt.

## Negative prompt
Do not overload the negative with 30 or more tags. A large negative becomes unpredictable. It is better to write a more accurate positive prompt.

Use this compact, reliable set as the default:

```
monochrome, greyscale, multiple views, text, watermark, signature, translation request, comic, 4koma, 2koma, lowres, worst quality
```

The first ten tags are the guide's reliable negative list. `lowres` and `worst quality` appear in its comparison example and are safe to keep. Add a term only for a problem you can see or reasonably expect. Do not start from a long inherited Pony or SDXL negative list.

## Camera, style and other useful tag groups
Use only the tags that match the image.

- **Camera and composition:** `straight-on`, `from side`, `from above`, `from below`, `three-quarter view`, `isometric`, `symmetry`, `full body`, `close-up`, `head out of frame`
- **Poses:** `sitting`, `standing`, `jumping`, `kneeling`, `on back`, `on side`, and clear arm or hand tags such as `arms up` or `hand on own hip`
- **Background and border:** `white background`, `halftone background`, `ornate frame`, and similar Danbooru background tags
- **Effects:** `blurry foreground`, `blurry background`, `depth of field`, `bloom`, `spot color`, only when they are actually visible
- **Medium and style:** `traditional media`, `watercolor (medium)`, `anime screenshot`, `1980s (style)`, `retro artstyle`, and similar documented tags. Mediums can be weighted, for example `(traditional media:0.5)`, when the user wants the style present but not dominant.

Avoid ambiguous or inconsistently used tags when a more precise tag exists. If a character has been redesigned and the old look is rare in the dataset, a LoRA may be needed; do not invent unofficial tags to force it.

## Tips
- Be specific. Name colors, garments and poses instead of vague adjectives.
- Give each person enough general tags that the model can keep them distinct. For two or more people, use the correct count tag and describe each person's hair, outfit and position before the shared background.
- If the source is a photograph, still write it as an anime or illustrated scene unless the user asks for a different medium, such as `photo (medium)`.
- The prompt format above is shared by base Illustrious and many popular finetunes. The guide prefers consistent community checkpoints over weaker official builds; use the same tag order either way.

## Example

Prompt for an illustration of a girl reading by a window. There is no named character or artist, and the SFW rating tag is omitted:

```
1girl, solo, wavy chestnut hair, shoulder length hair, hazel eyes, light freckles, gold hoop earrings, oversized cream sweater, sleeves pushed up, charcoal leggings, gray wool socks, slight smile, sitting, knees up, holding book, looking down, cowboy shot, from side, three-quarter view, window seat, rainy window, indoor, potted plant, mug, overcast daylight, lamp light, masterpiece, newest

Negative: monochrome, greyscale, multiple views, text, watermark, signature, translation request, comic, 4koma, 2koma, lowres, worst quality
```

## Source
[Illustrious Prompt Guide (Optimized & Complete)](https://civitai.com/articles/16016/illustrious-prompt-guide-optimized-and-complete)
