---
name: mmh3-prompting
description: Use when the user sends an image or describes a scene and wants a paste-ready MiniMax H3 (MMH3) video timeline. Turns the picture into a structured keyframe-completion prompt with subjects, timing, sound and camera.
---

# MMH3 Prompting

Turn any image (or a short scene description) into one faithful, paste-ready MiniMax H3 timeline. MiniMax H3, often called MMH3, is a video and audio model that follows a structured rewrite with labeled subjects, timed shots and a soundscape.

## When to use
- The user sends an image and asks for an MMH3 prompt, a MiniMax H3 timeline, or a short clip that starts from that still.
- The user describes a scene in words and wants it written as a MiniMax H3 prompt.

## How to respond
- Reply with a single timeline inside one code block, ready to paste. Use the section headings and label syntax exactly as shown below.
- When the user sends an image, treat it as `<Picture 1>`, the first frame at `00:00.000`. Keep identity, body, clothing, pose and place faithful to that still, then add motion that can grow from it.
- Ask a question only if the image cannot be read.
- Adult content follows the host platform's policies. Every person depicted must be an adult.
- Default to a 5 second clip unless the user names another length. Supported durations are typically 4 to 15 seconds. The last timestamp must match the requested length.

## Modes
- **I2VA / keyframe completion (default for a still image):** the image is the exact first frame. Use the six-section reference format below, with the summary starting `[keyframe completion]`.
- **T2VA:** text only, no reference still. You may use the same six sections and invent the opening frame in `detailed_description`, or a shorter base form with `integrated_multimodal_description`, `overall_soundscape` and `non_diegetic_music`. Prefer the six-section form if the user already expects that structure.
- **FL2VA:** the user supplies a first frame and a last frame. Describe a continuous path from one to the other. The final shot must arrive at the last frame.
- **L2VA:** the user supplies only a last frame. Infer a plausible opening and converge to that still.
- **Other reference tasks** such as video editing, video continuation, audio reuse or audio reference belong in the `summary` prefix, combined with `+` when more than one applies. Use them only when the user actually provides those assets.

## Format (default: image as first frame)

Write these six sections in this order, with a blank line between sections. Keep every reference label consistent across the whole timeline.

### 1. `subject_definitions`
Give each referenced item its own line.

- `<Subject N> is the [girl / man / other] already in <Picture 1>,` followed by the appearance, outfit and starting pose that must be preserved.
- `<Picture 1> is the reference still. It locks identity, body, pose, clothing, and place. It is the frame at 00:00.000.`

Only define a picture or video as its own line when it is a concrete frame or a source asset you will mention again. Write in English. Keep any spoken words, lyrics or on-screen text in their original language.

### 2. `summary`
One short paragraph that begins with a bracketed task type, then describes the clip. For a still used as the first frame:

```
[keyframe completion] A 5 second clip that starts on <Picture 1> and follows <Subject 1> as she turns a page and glances at the rain.
```

Valid task types include `keyframe completion`, `reference generation`, `video editing`, `video continuation`, `audio reuse` and `audio reference`.

### 3. `retention_analysis`
One line per defined label. For subjects, pictures and videos use only `fully_preserved`, `partially_preserved`, `attribute_transfer` or `weak_reference`. For a first-frame still, both the subjects and `<Picture 1>` are usually `fully_preserved`, with a short list of the traits and setting details that stay locked.

### 4. `detailed_description`
Start with the art style that matches the image, then say it is already present in `<Picture 1>` and is kept identical for the whole clip.

Describe a single continuous take unless the user asks for cuts. Use timed shot lines in playback order:

```
[Shot 1] 00:00.000 The clip starts exactly on <Picture 1>: ...
[Shot 1] 00:01.500 ...
[Shot 1] 00:03.000 ...
[Shot 1] 00:05.000 ..., as the single continuous take ends.
```

At `00:00.000`, restate the first frame clearly. Later lines should show observable motion: body, hair, hands, cloth, props, expression and camera. End on a held beat at the final timestamp. Name the camera angle and whether it holds steady or moves. Do not use old bracket camera commands such as `[Push in]`.

### 5. `overall_soundscape`
The diegetic sound of the place and the people: room tone, weather, footsteps, cloth, breaths, spoken words. Keep it consistent with the picture.

### 6. `non_diegetic_music`
Background music heard only by the audience. Write `none` unless the user asks for a score, in which case describe style, tempo and how it sits under the clip.

## Tips
- Be specific and visual. Name colors, materials, positions and sounds.
- Give each subject a full appearance so identity stays stable.
- Pick motion a body can actually perform from the first frame. Build it over the clip instead of jumping to a new pose.
- Match the timestamps to the requested duration. Do not leave a label undefined, and do not mention a label you never defined.
- Prefer concrete visual and audio detail over vague words such as "cinematic" or "beautiful."

## Example

Timeline for a 5 second clip that starts on a photo of a girl reading by a window:

```
subject_definitions:
<Subject 1> is the girl already in <Picture 1>, a young adult with an oval face, soft hazel eyes, light freckles, a calm closed lip smile, shoulder length wavy chestnut hair tucked behind one ear, small gold hoop earrings, an oversized cream knit sweater with the sleeves pushed to her elbows, charcoal leggings and thick gray wool socks, sitting curled on a cushioned window seat with a hardcover book open against her knees and a mug of tea beside her.
<Picture 1> is the reference still. It locks identity, body, pose, clothing, and place. It is the frame at 00:00.000.

summary:
[keyframe completion] A 5 second clip that starts on <Picture 1> and follows <Subject 1> as she turns a page and glances at the rain, then looks back down at the book.

retention_analysis:
<Subject 1>: fully_preserved oval face, soft hazel eyes, light freckles, shoulder length wavy chestnut hair, gold hoop earrings, oversized cream knit sweater, charcoal leggings, gray wool socks, sitting curled on the window seat with the book and mug
<Picture 1>: fully_preserved cozy reading nook, rain streaked window, sage green cushions, knitted throw, stack of books, trailing pothos plant, mug of tea, cool daylight and a warm lamp

detailed_description:
Photorealistic live action, already present in <Picture 1>, kept identical for the whole clip.
[Shot 1] 00:00.000 The clip starts exactly on <Picture 1>: <Subject 1> sits curled on the window seat, the hardcover book open against her knees, her gaze on the page.
[Shot 1] 00:01.500 She turns the page with her right hand, the sweater sleeve shifting at her elbow, while the rain continues on the glass.
[Shot 1] 00:03.000 She glances toward the rain streaked window, then looks back down at the book with a calm closed lip smile.
[Shot 1] 00:05.000 She holds that quiet look at the page, the mug still beside her, as the single continuous take ends.

overall_soundscape:
Quiet reading nook, rain against the window, the soft rustle of a turning page, <Subject 1>'s calm breathing.

non_diegetic_music:
none
```
