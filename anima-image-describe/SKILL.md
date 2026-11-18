---
name: anima-image-describe
description: Use when the user sends an image and wants it described as a paste-ready Anima prompt. Turns any picture into a hybrid prompt using official tag order plus two spatial prose sentences, with a compact negative prompt.
---

# Anima Image Describe

Turn any image into one faithful, paste-ready Anima prompt that describes the picture for what it is. Anima is a 2B anime and illustration model from CircleStone Labs and Comfy Org. It understands tags, natural language, and a mix of the two. It is meant for illustrations and artistic images, not photorealism.

This skill follows the hybrid prompt formula, tag order, syntax, quality prefixes, and negative-prompt advice in [The Ultimate Anima Prompting Guidebook](https://civitai.com/articles/35368/the-ultimate-anima-prompting-guidebook-all-you-need).

## When to use
- The user sends an image and asks you to describe it, recreate it, or turn it into an Anima prompt.
- The user describes a scene in words and wants it written as an Anima prompt.

## How to respond
- Reply with a single prompt inside one code block, ready to paste. Include a short negative prompt under a `Negative:` line in the same block.
- Describe what is actually in the image. Keep the subjects, clothing, pose, setting, colors, lighting and framing faithful to the source. Do not invent a different scene unless the user asks for changes.
- Ask a question only if the image cannot be read.
- Adult content follows the host platform's policies. Every person depicted must be an adult.

## Default: hybrid prompt
Use hybrid prompting as the default. Tags name the visual vocabulary. Prose places those elements in the frame and describes what they are doing.

There are two other official modes. Use them only when they clearly fit:
- **Tag-only** for a single subject, a familiar pose, and a simple composition.
- **Natural language only** for a scene whose meaning depends on relationships or action. Write at least two concrete sentences. Describe visible information, not lore or personality that has no visual consequence. Use ordinary English capitalization for character and series names.

## Format
Write one tag block, then two prose sentences, in this order:

Quality + era + safety → subject count → identity → series → artist or style → visible attributes → pose and action → camera → environment → lighting → natural-language spatial description

Reusable template:

```
[quality tags], [year or period], [meta tags], [safety tag], [subject count], [character name], [series], [@artist or medium/style], [hair], [eyes], [clothing], [expression], [pose/action], [camera/framing], [environment], [lighting/effects]. [Sentence 1: identify the main subject and place them in the frame.] [Sentence 2: describe the action, object relationships, depth, and important lighting.]
```

The official tag order inside the tag block is:

`[quality / meta / year / safety]` → `[subject count]` → `[character]` → `[series]` → `[artist]` → `[general tags]`

### Quality, year, meta and safety
If the user does not name a version, use the official Base prefix:

```
masterpiece, best quality, score_7, safe,
```

Add era and meta tags that match the image, such as `year 2025`, `newest`, and `highres`. Year and period tags (`newest`, `recent`, `mid`, `early`, `old`) are aesthetic controls, not factual timestamps.

If the user asks for Anima-Aesthetic, do not use `score_*` tags in the positive or the negative. A clean Aesthetic prefix is `safe, highres,` or `masterpiece, best quality, safe, highres,`.

Use a safety tag that matches the image: `safe`, `sensitive`, `nsfw`, or `explicit`. Keep the scene descriptive enough that the model is not left to invent missing details.

Useful meta tags include `highres`, `absurdres`, `anime screenshot`, and `official art`. Use only tags that belong in the documented vocabulary.

### Identity
For a known character, include three anchors: the character name, the series, and the basic visible appearance. Do not rely on the name alone. Use the canonical lowercase tag in the tag block, and normal capitalization in the prose.

For an original character, write a compact, stable identity packet (hair, eyes, defining accessories and clothing). Keep that packet consistent, and put temporary pose, weather and camera details outside it. Do not list conflicting synonyms such as several hair lengths or both glasses and no glasses.

### Artist and style
Add an artist tag only when the user asks for one. It must begin with `@`, for example `@artist name`. Without the `@`, the effect is very weak. Start with one artist. Style tags such as `anime coloring, clean lineart, soft cel shading` are often more stable than mixing several artists.

### Camera, background and lighting
Choose one clear option from each relevant camera category, and do not stack mutually exclusive angles:
- Framing: `close-up`, `upper body`, `cowboy shot`, `full body`, `wide shot`
- Angle: `from above`, `from below`, `eye level`, `from side`, `three-quarter view`
- Lens or composition, only if visible: `wide angle`, `telephoto`, `shallow depth of field`, `centered composition`

The background should include a location, one or two defining objects, a depth relationship, and the time or weather. Use lighting tags that can exist together, such as `sunset, warm backlighting, rim light`. Do not add every fashionable lighting tag at once.

### Natural-language block
After the tags, write two concrete sentences:
1. Identify the main subject and place them in the frame.
2. Describe the action, object relationships, depth, and important lighting.

Tags name objects; prose places them. Prefer "the girl occupies the lower right foreground, with the window rising behind her" over a bare list of nouns.

### Multi-character scenes
Start with the count and the shared scene. Then give each person their own sentence, with a clear position such as "the girl on the left" or "the man on the right," plus their appearance. End by restating the interaction and the environment. Do not dump both wardrobes before assigning them to positions, and do not rely on a comma-only list of names.

## Tag syntax
- Write visual tags in lowercase, with spaces rather than underscores. The exception is score tags, which keep the underscore: `score_7`.
- When Danbooru and Gelbooru spell a tag differently, use the Gelbooru form.
- Put a space after each comma: `1girl, solo, blue hair`, not `1girl,solo,blue hair`.
- Canonical Booru emote tags such as `;d`, `:3`, or `>_<` may be used for expression. Keep their exact spelling, including any underscore in the tag name. Use one primary emote. These control the face; they do not reliably print as text in the image.
- You do not need every possible tag. Anima was trained with tag dropout. Prioritize subject count, identity, defining appearance, pose, camera, environment, lighting and style.
- Do not combine incompatible tags unless the contradiction is intentional, such as `short hair` with `very long hair`, or `solo` with `2girls`.

## Weighting
Prompt weighting works, but Anima often needs a stronger value than typical SDXL. The official example is `(chibi:2)`. If a concept is weak, test `(tag:1.5)` and then `(tag:2)`. Use weights for a disappearing concept, a weak camera instruction, a style accent, or two non-contradictory ideas that compete. Do not use weights to repair an incoherent prompt, and do not weight several artists at once.

## Negative prompt
Start compact. For Base:

```
worst quality, low quality, score_1, score_2, score_3, artist name, blurry, jpeg artifacts, chromatic aberration
```

For Aesthetic, omit the `score_*` tags:

```
worst quality, low quality, artist name, blurry, jpeg artifacts, chromatic aberration
```

Add a term only for a failure you can see or reasonably expect, such as `extra fingers` or `extra person`. Do not start with a long inherited SDXL negative. Oversized negatives can strip detail or shift the result in unexpected ways.

## Tips
- Specificity matters more than length. Every important visual decision should have a clear owner.
- Be concrete. Name colors, garments, materials, positions and light.
- Anima does not do photorealism well. If the source is a photograph, write the prompt as an anime or illustrated scene unless the user insists on a photographic look.
- Anima is weak at long text in the image. You can ask for a single word or a short phrase.
- If a result goes wrong, change one module of the formula at a time instead of rewriting the whole prompt.

## Example

Prompt for an illustration of a girl reading by a window:

```
masterpiece, best quality, score_7, safe, year 2025, newest, highres, 1girl, solo, young adult, wavy chestnut hair, shoulder length hair, hazel eyes, light freckles, gold hoop earrings, oversized cream knit sweater, sleeves pushed up, charcoal leggings, gray wool socks, slight smile, sitting, knees up, holding book, looking down, cowboy shot, from side, three-quarter view, window seat, rainy window, indoor, potted plant, mug, overcast daylight, lamp light, anime coloring. A young adult girl sits curled on a cushioned window seat in the center of the frame, a hardcover book open against her knees and a mug of tea beside her. Cool daylight from the rain streaked window falls across her face and the pages, while a warm lamp at the left adds a soft rim along her hair, and a pothos and a stack of books recede along the sill behind her.

Negative: worst quality, low quality, score_1, score_2, score_3, artist name, blurry, jpeg artifacts, chromatic aberration
```

## Source
[The Ultimate Anima Prompting Guidebook (All you need)](https://civitai.com/articles/35368/the-ultimate-anima-prompting-guidebook-all-you-need)
