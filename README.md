# Image Describe Skills

Portable skills that turn a picture (or a short scene description) into one paste-ready prompt for a specific image or video model. Each skill lives in its own folder with a `SKILL.md` file, so you can add one model or all of them to an AI assistant.

The skills are generic. They describe what is actually in the image, follow that model's usual prompting style, and stay faithful to the source unless you ask for a change. Adult content follows the host platform's policies, and every person depicted must be an adult.

## Skills

| Folder | Model | What it writes |
| --- | --- | --- |
| `illustrious-image-describe` | Illustrious (SDXL anime) | A Danbooru-style tag prompt with important identity tags first, `masterpiece, best quality` at the end of long prompts, and a compact `worst quality, low quality` negative |
| `anima-image-describe` | Anima (CircleStone Labs / Comfy Org) | A hybrid prompt in official tag order (quality, era, safety, count, identity, attributes, pose, camera, environment, lighting), then two spatial prose sentences, plus a compact negative prompt |
| `krea-image-describe` | Krea | Three prose paragraphs covering style and subjects, location and lighting, then camera and composition |
| `moss-image-describe` | MOSS-Image (OpenMOSS) | A detailed English caption by default, with optional tag sequences or JSON layout when placement or anime tags fit better, plus a negative prompt |
| `wan22-image-to-video` | Wan 2.2 | A 5 second image-to-video timeline: a scene paragraph, timed `0-1s` through `4-5s` beats, then `Motion:` and `Negative:` lines |
| `mmh3-prompting` | MiniMax H3 (MMH3) | A structured video timeline with subject labels, a keyframe-completion summary, timed shots, soundscape and music |

## How to add these skills to an AI

Each skill is a folder that contains a single `SKILL.md`. The file starts with YAML frontmatter (`name` and `description`) and then the instructions. Copy the folder you want, or the whole repository.

### Claude / Claude Code

Copy a skill folder into your personal or project skills directory so the path looks like this:

```text
~/.claude/skills/krea-image-describe/SKILL.md
```

Use the folder name as the directory name. Restart or refresh the session if the new skill does not appear. Claude Code also picks up skills from a project's `.claude/skills/` folder, which is a good way to share them with a repo.

### Cursor and Grok Bot

Copy the skill folder into the agent's skills or workflows directory (the location your setup already uses for `SKILL.md` files). The frontmatter `name` and `description` tell the agent when to load it. After the folder is in place, send an image and ask for a prompt in that model's style.

### ChatGPT custom GPTs and projects

Open the custom GPT or project instructions and paste the contents of the `SKILL.md` you want to use. If you want more than one model, paste each skill under a clear heading, and tell the GPT to pick the skill that matches the user's request. You can also attach the `SKILL.md` as a project file and ask the model to follow it.

### Any other assistant

Paste the `SKILL.md` into the system prompt, the custom instructions, or a pinned document, then tell the assistant to follow it when you send an image. If the host supports skill folders, keep the `SKILL.md` inside a folder named after the skill.

## Usage

Send an image (or describe a scene) and name the model, for example:

- "Describe this as a Krea prompt."
- "Write an Illustrious prompt and negative for this image."
- "Turn this still into a Wan 2.2 timeline."
- "Write an MMH3 timeline that starts on this frame."

The assistant should return one paste-ready prompt in a code block, in that model's format, describing the picture faithfully.

If you only want a description in one style, add only that skill. If you work with several models, install all of the folders and name the model in your request.

## License

MIT. See [LICENSE](LICENSE).
