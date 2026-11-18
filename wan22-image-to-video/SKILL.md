---
name: wan22-image-to-video
description: Use when the user sends an image or describes a scene and wants a paste-ready Wan 2.2 image-to-video timeline. Turns the picture into a 5 second timeline with a scene paragraph, timed beats, a Motion line and a Negative line.
---

# Wan 2.2 Image to Video

Turn any image (or a short scene description) into one faithful, paste-ready Wan 2.2 timeline. Wan 2.2 is a natural-language video model. The default output is a 5 second image-to-video timeline, not a single paragraph and not a tag list.

## When to use
- The user sends an image and asks for a Wan 2.2 prompt, an image-to-video prompt, a Wan timeline, or a short clip that starts from that still.
- The user describes a scene in words and wants it written as a Wan 2.2 timeline.

## How to respond
- Reply with a single timeline inside one code block, ready to paste. Use the section layout and field names exactly as shown below.
- Treat the image as the first frame. Describe the people, clothing, pose and setting faithfully in the opening paragraph, then add motion in the timed beats that can grow naturally from that still. Do not invent a different scene unless the user asks for changes.
- Ask a question only if the image cannot be read.
- Adult content follows the host platform's policies. Every person depicted must be an adult.
- Default to a 5 second clip with five 1 second beats unless the user names another length.

## Format
Write the timeline in this order, with a blank line after the scene paragraph and a blank line after the last beat.

### 1. Scene paragraph
One short natural-language paragraph that locks the first frame. Cover:

1. The setting, time of day and lighting.
2. Each person or main subject: apparent age, hair, face, outfit and the starting pose as seen in the still. With several people, refer to them as "the first girl", "the second girl", "the man", and so on, and give each one enough detail to stay distinct.
3. The art style only when it is needed to match the image, such as "Photorealistic live action footage" or "Anime style animation with clean linework." Do not add quality tags or trigger words.

If the image contains visible text, state the exact words and where they appear, and keep that text stable unless the user wants it to change. Do not put the clip's later action or the camera move in this paragraph. Those belong in the beats and the `Motion:` line.

### 2. Timed beats
Five lines, one second each, using hyphens in the labels (not en dashes or em dashes):

```
0-1s: ...
1-2s: ...
2-3s: ...
3-4s: ...
4-5s: ...
```

Each beat is one or two concrete actions a body can actually perform from the previous beat. Build the motion instead of jumping to a new pose. Keep identity, outfit and setting stable. The first beat should start from the still. The last beat should land on a clear held moment.

If the user asks for a different length, keep 1 second beats (or even divisions) that add up to that length, and use the same `N-Ms:` label style.

### 3. `Motion:`
One line that starts with `Motion:`. Describe how the camera behaves and how the motion of the clip feels as a whole. Pick one clear camera behavior and stick to it. Name the angle and height so they match the source image. Examples:

- `Motion: The camera is steady and still at eye level. She moves in a continuous slow rhythm, her hair shifting softly.`
- `Motion: The camera holds a steady eye level three quarter view from inside the room, with a slight natural sway.`
- `Motion: Handheld camera with a slight natural sway. The camera tracks with him as he walks.`

Do not mix several competing camera moves in a short clip. Do not use old bracket camera commands such as `[Push in]`.

### 4. `Negative:`
One line that starts with `Negative:`. List things the clip should not do. Start with whatever would break the starting pose or the intended action (for example `standing up, leaving the seat, covering the book`), then add a short technical set:

```
static, frozen, blurry, distorted anatomy, extra fingers, morphing face, changing hair, clothing changes, camera cuts, zoom, text, watermark, logo, low quality, jitter
```

Keep the list short and relevant. Do not paste a long kitchen-sink negative.

## Tips
- Be specific and visual. Name colors, materials and positions.
- Motion should be simple and readable: a glance, a page turn, hair lifting in a breeze, a few steps, a smile forming. Overloading a 5 second clip makes the result messy.
- Keep identity, outfit and setting stable unless the story of the clip requires a change.
- Describe only motion that can start from the still. Do not teleport a subject or snap the camera to a new shot unless the user asks for a cut.
- Do not use quality tags, LoRA trigger words, or a single-paragraph prompt as the default. The timeline is the default output.

## Example

Timeline for a 5 second clip that starts on a photo of a girl reading by a window:

```
A cozy reading nook on a rainy afternoon, soft cool daylight from a tall rain streaked window and a warm lamp at the left. A young adult girl sits curled on a cushioned window seat, an oval face, soft hazel eyes, light freckles and shoulder length wavy chestnut hair tucked behind one ear, wearing an oversized cream knit sweater, charcoal leggings and thick gray wool socks, a hardcover book open against her knees and a mug of tea beside her.

0-1s: She reads quietly, her eyes moving down the page.
1-2s: She turns the page with her right hand, the sweater sleeve shifting at her elbow.
2-3s: She glances toward the rain streaked window as the pothos leaves stir in the draft.
3-4s: She looks back down at the book with a calm closed lip smile.
4-5s: She holds that quiet look at the page, the mug still beside her.

Motion: The camera is steady and still at eye level in a three quarter view from inside the room. She moves in a continuous slow rhythm, the rain continuing on the glass.

Negative: standing up, leaving the seat, closing the book, covering up, turning away, fast motion, extra hands, extra people, static, frozen, blurry, distorted anatomy, extra fingers, morphing face, changing hair, clothing changes, camera cuts, zoom, text, watermark, logo, low quality, jitter
```
