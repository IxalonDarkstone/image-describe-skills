---
name: illustrious-image-describe
description: Use when the user sends an image and wants it described as a paste-ready Illustrious (SDXL anime) prompt. Turns any picture into a faithful Danbooru-style tag prompt, with important identity tags first and a compact negative prompt.
---

# Illustrious Image Describe

Turn any image into one faithful, paste-ready Illustrious prompt that describes the picture for what it is. Illustrious is a fine-tuned SDXL anime model trained on Danbooru tags. It is not Pony, and it does not use Pony score tags.

This skill follows the prompting structure, quality tags, and negative-prompt advice in [Arctenox's Simple Prompt Guide for Illustrious for ComfyUI/Site](https://civitai.com/articles/23210/arctenoxs-simple-prompt-guide-for-illustrious-for-comfyuisite). That guide is written for base Illustrious and may not be exact on every merge or finetune.

## When to use
- The user sends an image and asks you to describe it, recreate it, or turn it into an Illustrious prompt.
- The user describes a scene in words and wants it written as an Illustrious tag prompt.

## How to respond
- Reply with a single prompt inside one code block, ready to paste. Include a short negative prompt under a `Negative:` line in the same block.
- Describe what is actually in the image. Keep the subjects, clothing, pose, setting, colors, lighting and framing faithful to the source. Do not invent a different scene unless the user asks for changes.
- Ask a question only if the image cannot be read.
- Adult content follows the host platform's policies. Every person depicted must be an adult.

## Format
Write comma-separated Danbooru-style tags. Use tags as they appear on Danbooru, not guessed spellings. Spaces or underscores are both accepted (`long hair` or `long_hair`); pick one and stay consistent.

Illustrious has a limited token budget (about 248 tokens without layering). Tags later in the prompt are more diluted and more easily forgotten, so put the important visual facts first.

Use this order:

1. **Subject count and identity:** `1girl`, `1boy`, `1other`, `2girls`, `solo`, then the character tag and series tag if a known character is clearly intended
2. **Appearance:** hair, eyes, skin, distinctive features, makeup, jewelry
3. **Outfit:** every visible garment with its color, plus shoes or barefoot
4. **Expression, pose and action:** what the subject is doing and how they are held in the frame
5. **Setting, lighting and composition:** location, time of day, light, and framing tags such as `cowboy shot`, `upper body`, `full body`, `from side`, `from above`, `looking at viewer`
6. **Quality tags,** placed according to prompt length (see below)

If the image contains visible text, add a short tag or a brief quoted phrase for the exact words.

### Quality tags
Do not use Pony `score_*` tags. Illustrious does not understand them.

The standard positive quality tags are:

```
masterpiece, best quality
```

- For a short prompt, these may go at the beginning.
- For a long prompt, especially one that has to protect an original character or a detailed identity, put `masterpiece, best quality` at the end so the identity tags at the front stay strong.

A faithful image-describe prompt is often long, so default to putting the quality tags at the end unless the tag list is short.

### Character and color tags
Use the character name in Danbooru order, not Western inverted order. For example, use `ash ketchum` or `ash_ketchum`, not `ketchum ash`.

Name colors specifically when you can see them. `dark blue sweater` is more precise than `blue sweater`, which may follow the model's default blue. Ordinary SDXL color words work on Illustrious.

If a Danbooru tag contains parentheses, such as `vex (lol)`, escape the parentheses so they are not read as prompt weights. In ComfyUI and on many sites that looks like `vex /(lol/)` or `vex_/(lol/)`.

Prefer tags that are well attested on Danbooru. A rare artist or concept with very few images may not hold, and may need a LoRA instead of a bare tag. Check unfamiliar tags on the [Danbooru tag list](https://danbooru.donmai.us/tags) or [artist list](https://danbooru.donmai.us/artists).

### Natural language
Prompts should stay tag-first. Models whose CLIP is Illustrious 2.0 or Illustrious 2.0 Stable can accept a little natural language, but only a short caption. Pre-2.0 checkpoints such as many WAI-Illustrious builds will not understand that caption the same way. If you add prose, keep it to one short sentence after the tags, and only when a spatial relationship is hard to express in tags.

## Negative prompt
Start compact:

```
worst quality, low quality
```

Sometimes a short prompt needs nothing more. Add a term only for something you do not want in this image, or for a failure you can see or reasonably expect, such as `bad hands`, `extra digits`, `jpeg artifacts`, `signature`, or `watermark`. Do not start with a long inherited Pony or SDXL negative list. Check unfamiliar negative tags on Danbooru or against what SDXL actually understands.

## Tips
- Be specific. Name colors, garments and poses instead of vague adjectives.
- Give each person enough early tags that the model can keep them distinct. For two or more people, use count tags and describe each person's hair, outfit and position before the shared background.
- Do not pad the prompt with quality fluff such as `8k` or `ultra detailed`, and do not use score tags.
- If the source is a photograph, still write it as an anime or illustrated scene unless the user asks for a different medium.
- A recommended CFG range for many Illustrious checkpoints is about 3 to 6. Settings above 6 often overcook the image. Mention this only if the user asks about settings.

## Example

Prompt for an illustration of a girl reading by a window. The tag list is long, so the quality tags sit at the end:

```
1girl, solo, young adult, oval face, hazel eyes, long eyelashes, straight eyebrows, light freckles, closed mouth, slight smile, shoulder length wavy chestnut hair, hair behind ear, gold hoop earrings, oversized cream sweater, sleeves pushed up, charcoal leggings, gray wool socks, sitting, knees up, holding book, looking down, window seat, rainy window, sage green cushions, knitted throw, stack of books, potted plant, mug, indoor, overcast daylight, lamp light, cowboy shot, from side, three-quarter view, masterpiece, best quality

Negative: worst quality, low quality
```

## Source
[Arctenox's Simple Prompt Guide for Illustrious for ComfyUI/Site](https://civitai.com/articles/23210/arctenoxs-simple-prompt-guide-for-illustrious-for-comfyuisite)
