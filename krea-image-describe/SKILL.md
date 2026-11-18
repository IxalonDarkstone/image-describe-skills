---
name: krea-image-describe
description: Use when the user sends an image and wants it described as a paste-ready Krea image prompt. Turns any picture into a faithful three paragraph prompt covering style, subjects, action, setting, lighting, camera and composition.
---

# Krea Image Describe

Turn any image into one faithful, paste-ready Krea prompt that describes the picture for what it is.

## When to use
- The user sends an image and asks you to describe it, recreate it, or turn it into a prompt.
- The user describes a scene in words and wants it written as a Krea prompt.

## How to respond
- Reply with a single prompt inside one code block, ready to paste.
- Describe what is actually in the image. Keep the subjects, clothing, pose, setting, colors, lighting and framing faithful to the source. Do not invent a different scene unless the user asks for changes.
- Ask a question only if the image cannot be read.

## Format
Write three paragraphs of natural prose, separated by a blank line. Do not use labels, bullet points or quality tags.

### Paragraph 1: Style, setting and subjects
1. Open with the art style that matches the image, followed by the setting. Examples: "Photorealistic photograph, inside a sunlit kitchen in the morning." or "Semi realistic digital painting with soft painterly rendering, inside a clinic office during the day." or "Anime style illustration with clean linework and bright cel shading, on a rooftop at sunset."
2. Introduce each person or main subject with their apparent age and how many there are. Example: "A young adult girl sits on a stool..." With several people, refer to them as "the first girl", "the second girl", "the man", and so on.
3. For each person, describe:
   - **Face:** face shape, eyes and eye color, brows, lips, expression lines, freckles, makeup.
   - **Hair:** color, length, texture and style, bangs, accessories.
   - **Skin:** tone, tan or flush, tattoos, piercings, jewelry.
   - **Body:** build, proportions and posture.
   - **Outfit:** every garment with its color, material, fit and how it is worn, plus shoes or bare feet.
4. Describe the pose (where the body, arms, hands, legs and feet are) and the action (what each person is doing, and how they interact or touch).
5. Close with each person's expression: their gaze direction, eyes, mouth and mood.
6. If the image contains visible text (a sign, a caption, a screen), state the exact words and where they appear.

### Paragraph 2: Location and lighting
1. Describe the location: the room or landscape, furniture, props, background details and colors.
2. Describe the light: the key light source and its direction, color temperature, rim light, fill, shadows and atmosphere.
3. End with a short time of day sentence, such as "Early evening." or "Late night."

### Paragraph 3: Camera and composition
1. Give the camera angle and height (eye level, low angle, high angle, overhead, three quarter, side profile, rear view, selfie view) and the shot size (close up, medium shot, full body).
2. Give the lens, for example "35mm lens" or "85mm lens".
3. Write "vertical frame with ..." (or horizontal or square, to match the image) and map where each element sits: top, upper left, center, lower right, along the bottom, and so on.
4. Give the depth of field, saying what is sharp and what is blurred.
5. End with a short finishing line that fits the style, such as "smooth painterly shading and clean defined anatomy." or "natural skin texture and sharp focus."

## Tips
- Be specific and visual. Name colors, materials and positions instead of using vague adjectives.
- Give each person their own full description so the model keeps them distinct.
- Pick pose descriptions that a body can actually hold. A body facing away while the face looks straight back at the camera often renders as an unnatural twist, so prefer a side profile, a gentle glance back, or a face seen in a mirror.
- Keep the details consistent across all three paragraphs. The composition map should mention the same items the first two paragraphs describe.

## Example

Prompt for a photo of a girl reading by a window:

```
Photorealistic photograph, inside a cozy reading nook on a rainy afternoon. A young adult girl sits curled on a cushioned window seat, seen in a three quarter view. She has an oval face, soft hazel eyes with long lashes, straight brows, light freckles across her nose and a calm closed lip smile, with shoulder length wavy chestnut hair tucked behind one ear and small gold hoop earrings. She has a slim build and relaxed posture. She wears an oversized cream knit sweater with the sleeves pushed to her elbows, charcoal leggings and thick gray wool socks. She sits with her knees drawn up, a hardcover book open against them, one hand holding the page and the other resting on a mug of tea beside her. She gazes down at the book, absorbed and peaceful.

The nook has a tall rain streaked window, sage green cushions, a knitted throw, a stack of books on the sill and a trailing pothos plant. Soft cool daylight from the window falls across her face and the pages, warm lamp light from the left adds a gentle rim along her hair, and soft shadows fill the corners. Rainy afternoon.

Eye level three quarter view from the room, medium shot, 50mm lens, vertical frame with the rainy window and plant along the top, her face and chestnut hair at the upper center, the open book and her hands at the center, the mug of tea at the lower right, and the cushions and wool socks along the bottom; shallow depth of field keeping her face and the book sharp and the window softly blurred, natural skin texture and sharp focus.
```
