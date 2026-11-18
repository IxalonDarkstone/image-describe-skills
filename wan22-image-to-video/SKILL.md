---
name: wan22-image-to-video
description: Use when the user sends an image or describes a scene and wants a paste-ready Wan 2.2 image-to-video prompt. Turns the picture into one natural-language paragraph covering subject, motion and camera.
---

# Wan 2.2 Image to Video

Turn any image (or a short scene description) into one faithful, paste-ready Wan 2.2 prompt. Wan 2.2 is a natural-language video model. A single paragraph that covers the subject, the motion, and the camera works better than tag lists.

## When to use
- The user sends an image and asks for a Wan 2.2 prompt, an image-to-video prompt, or a short clip that starts from that still.
- The user describes a scene in words and wants it written as a Wan 2.2 prompt.

## How to respond
- Reply with a single prompt inside one code block, ready to paste. One paragraph, no labels, no bullet points, no tag lists.
- Treat the image as the first frame. Describe the people, clothing, pose and setting faithfully, then add motion that can grow naturally from that still. Do not invent a different scene unless the user asks for changes.
- Ask a question only if the image cannot be read.
- Adult content follows the host platform's policies. Every person depicted must be an adult.
- Default to a short clip of about 5 seconds unless the user names another length.

## Format
Write one natural-language paragraph in this order:

1. **Style and medium.** Open with the art style that matches the image, plus the word `animation` (or `live action` if the source is photographic footage). Examples: "Photorealistic live action footage," or "Semi realistic digital painting animation with soft painterly rendering," or "Anime style animation with clean linework and bright cel shading."
2. **Setting.** Where the action takes place, in a short phrase.
3. **Subjects.** Introduce each person or main subject with their apparent age, hair, face, outfit and pose as seen in the first frame. With several people, refer to them as "the first girl", "the second girl", "the man", and so on, and give each one enough detail to stay distinct.
4. **Motion.** Describe what happens over the clip, in time order, as actions a body can actually perform from the starting pose. Build the motion rather than jumping to a new pose. Keep the action continuous and physically plausible.
5. **Camera, light and finish.** Close with how the camera moves or holds, the lighting, and a short motion-quality line such as "smooth natural motion."

If the image contains visible text, state the exact words and where they appear, and keep that text stable unless the user wants it to change.

## Camera language
Pick one clear camera behavior and stick to it:

- `The camera holds a steady eye level three quarter view...`
- `The camera slowly pans right...`
- `The camera eases in toward her face...`
- `The camera tracks with him as he walks...`
- `Handheld camera with a slight natural sway...`

Name the angle and height (eye level, low angle, high angle, overhead, side profile, selfie view) so they match the source image. Do not mix several competing camera moves in a short clip.

## Tips
- Be specific and visual. Name colors, materials and positions.
- Motion should be simple and readable: a glance, a page turn, hair lifting in a breeze, a few steps, a smile forming. Overloading a 5 second clip makes the result messy.
- Keep identity, outfit and setting stable unless the story of the clip requires a change.
- Describe only motion that can start from the still. Do not teleport a subject or snap the camera to a new shot unless the user asks for a cut.
- Do not use quality tags, LoRA trigger words, or old bracket camera commands.

## Example

Prompt for a short clip that starts on a photo of a girl reading by a window:

```
Photorealistic live action footage, inside a cozy reading nook on a rainy afternoon. A young adult girl sits curled on a cushioned window seat, an oval face, soft hazel eyes, light freckles and shoulder length wavy chestnut hair tucked behind one ear, wearing an oversized cream knit sweater, charcoal leggings and thick gray wool socks, a hardcover book open against her knees and a mug of tea beside her. She reads quietly, then turns a page with her right hand, glances toward the rain streaked window, and looks back down at the book with a calm closed lip smile as the pothos leaves shift in the draft. The camera holds a steady eye level three quarter view from inside the room, soft cool window light and a warm lamp at the left, smooth natural motion.
```
