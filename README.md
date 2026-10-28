# AI Comic Prompt Skill

AI Comic Prompt Skill is a model-aware prompt engineering toolkit for AI-assisted comic production. It transforms storyboards, scene descriptions, character references, and existing tag strings into concise prompts that are ready to adapt to an image-generation workflow.

## NAI v4.5 Prompt Assistant

The current release, [`nai-v45-comic-prompt`](skills/nai-v45-comic-prompt/), is specialized for NovelAI Diffusion V4.5 Full and Curated. It is designed for comic panels and multi-shot sequences where composition, character continuity, and prompt order matter.

### Core capabilities

- Convert natural-language shot descriptions and supplied tag strings into compact mixed tag-and-language prompts.
- Separate each output into a global scene prompt and one prompt per visible character.
- Encode camera distance, framing, angle, viewpoint, subject placement, visible props, lighting, and interactions.
- Track visible clothing, accessories, hairstyle, facial expression, gaze, pose, action, and character-to-scene interactions.
- Rebuild prompts for every shot instead of copying a fixed character block across changing camera crops.
- Remove details that fall outside the current crop, such as lower-body details in an upper-body close-up.
- Prioritize composition-critical information according to NAI prompt-order behavior and remove redundant phrasing.
- Prefer established Danbooru-style tags while reserving short natural language for precise relationships and staging.
- Keep artist strings and quality boilerplate outside the copyable prompt output.
- Provide a Chinese reference translation below each English prompt block.
- Run a structured self-check for model target, crop alignment, composition, interactions, ordering, and redundancy.

## Typical workflow

Provide any combination of:

- a storyboard or shot description;
- character baseline tags or prompt fragments;
- existing prompt strings to preserve or revise;
- previous and following shots for continuity;
- the requested model and generation mode when it differs from NAI v4.5.

The assistant first identifies the facts visible in the current shot, then builds a shot-specific prompt inventory. The final response presents copyable prompt blocks for the scene and each character, followed by Chinese reference translations and a self-check. A continuity base can be maintained internally across a sequence and revised for each individual shot.

## Scope

Version 1 is a pure prompt-writing skill. It does not operate ComfyUI, call image-generation APIs, edit image metadata, control Photoshop, or automate clipboard actions. Model-specific prompt rules remain isolated so that future skills can support other checkpoints and platforms without changing the NAI v4.5 contract.

## Installation

Use the self-contained skill directory with an agent runtime that supports skills:

```text
skills/nai-v45-comic-prompt/
├── SKILL.md
├── agents/openai.yaml
└── references/model-notes.md
```

Copy `skills/nai-v45-comic-prompt/` into the runtime's skill directory, or load the directory according to the runtime's skill configuration. No API key, image service credential, or ComfyUI connection is required for the current release.

## Repository direction

Additional model and production-tool skills will be added as independent directories. Planned extensions include optional MUV-style structured input constraints, ComfyUI MCP execution and result iteration, and integrations for image editing and manga layout. These are future extensions; the current release remains focused on reliable NAI v4.5 prompt construction.
