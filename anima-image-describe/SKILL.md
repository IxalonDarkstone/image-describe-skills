---
name: anima-image-describe
description: Use when the user sends an image and wants it described as a paste-ready Anima prompt. Turns any picture into a faithful hybrid of Danbooru-style tags and a short natural-language caption.
---

# Anima Image Describe

Turn any image into one faithful, paste-ready Anima prompt that describes the picture for what it is. Anima is a 2B anime and illustration model from CircleStone Labs and Comfy Org. It is trained on Danbooru-style tags, natural-language captions, and mixtures of the two. It is meant for illustrations and artistic images, not photorealism.

## When to use
- The user sends an image and asks you to describe it, recreate it, or turn it into an Anima prompt.
- The user describes a scene in words and wants it written as an Anima prompt.

## How to respond
- Reply with a single prompt inside one code block, ready to paste. Include a short negative prompt under a `Negative:` line in the same block.
- Describe what is actually in the image. Keep the subjects, clothing, pose, setting, colors, lighting and framing faithful to the source. Do not invent a different scene unless the user asks for changes.
- Ask a question only if the image cannot be read.
- Adult content follows the host platform's policies. Every person depicted must be an adult.

## Format
Write a hybrid prompt: a tag prefix, then two or more descriptive sentences.

### Tag prefix
Use lowercase tags with spaces instead of underscores. The only tags that keep underscores are score tags such as `score_7`.

Recommended order:

1. **Quality, meta, year and safety:** `masterpiece, best quality, score_7, highres, year 2025, newest`, plus a safety tag that matches the image (`safe`, `sensitive`, `nsfw`, or `explicit`)
2. **Subject count:** `1girl`, `1boy`, `1other`, `2girls`, `solo`, and so on
3. **Character and series,** if a known character is clearly intended
4. **Artist,** only when the user asks for one: prefix the name with `@`, for example `@artist name`. The `@` is required or the effect is very weak.
5. **General tags:** hair, eyes, outfit, expression, pose, framing, setting and lighting

When a tag is spelled differently on Danbooru and Gelbooru, prefer the Gelbooru spelling.

For Anima-Aesthetic, quality tags in the positive are optional. `masterpiece, best quality` is safe to leave in. Skip `score_*` tags in both the positive and the negative, because they can push the aesthetic model too hard. For Anima-Base or a generic Anima prompt, the quality and score prefix above is a good default.

### Natural language
After the tags, write at least two sentences in ordinary English. Cover mood, pose, composition, lighting and any details the tags only sketched. Follow normal capitalization for character and series names. Name a character, then describe their basic appearance, especially when more than one person is in the scene.

You may mix tags and sentences in any order. A clean default is: quality and subject tags first, then the sentences.

### Weighting
Prompt weighting works, but it needs a stronger value than typical SDXL. Example: `(chibi:2)`.

## Negative prompt
Recommended default:

```
worst quality, low quality, score_1, score_2, score_3, artist name, blurry, jpeg artifacts, chromatic aberration
```

For Anima-Aesthetic, omit the `score_*` tags from the negative as well.

## Tips
- More description is better. Extremely short prompts can give unexpected results.
- Be specific. Name colors, garments, materials and positions.
- Give each person their own appearance so the model keeps them distinct.
- Anima does not do photorealism well. Even if the source is a photo, write the prompt as an anime or illustrated scene unless the user insists on a photographic look.
- Anima is weak at long text in the image. You can ask for a single word or a short phrase. Do not rely on it for paragraphs of lettering.
- You do not need every possible tag. The model was trained with tag dropout, so a focused set plus clear sentences is enough.
- Optional dataset tags exist for non-anime art styles. A prompt may begin with `ye-pop` or `deviantart` on its own line when the source is a painterly or mixed illustration rather than anime. Use this only when it matches the image.

## Example

Prompt for an illustration of a girl reading by a window:

```
masterpiece, best quality, score_7, highres, year 2025, newest, safe, 1girl, solo, young adult, oval face, hazel eyes, long eyelashes, light freckles, slight smile, shoulder length wavy chestnut hair, hair tucked behind ear, gold hoop earrings, oversized cream knit sweater, sleeves pushed up, charcoal leggings, gray wool socks, sitting, knees up, holding book, looking down, window seat, rainy window, indoor, potted plant, mug, cowboy shot, from side. A young adult girl sits curled on a cushioned window seat with a hardcover book open against her knees and a mug of tea beside her. Cool daylight from the rain streaked window falls across her face and the pages, with a warm lamp adding a soft rim along her hair.

Negative: worst quality, low quality, score_1, score_2, score_3, artist name, blurry, jpeg artifacts, chromatic aberration
```
