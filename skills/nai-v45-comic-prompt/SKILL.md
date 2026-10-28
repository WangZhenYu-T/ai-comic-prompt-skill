---
name: nai-v45-comic-prompt
description: Generate concise, shot-aware NovelAI Diffusion V4.5 comic prompts from scene descriptions, character tags, reference tag strings, and storyboard context. Use when the user wants layered global scene and per-character prompts in Danbooru-style tags plus limited natural language, with Chinese translations, camera-aware tag pruning, prompt-order prioritization, and a mandatory self-check. This skill targets NAI V4.5; adapt or warn before using it for other models.
---

# NAI v4.5 Comic Prompt Assistant

## Operating contract

Act as a prompt editor for comic storyboards. Produce prompts that can be pasted into a generation workflow, not a long visual rewrite. Treat the user's supplied tags, prose, and reference strings as the source of truth; never invent missing character facts just to fill a template.

Target NovelAI Diffusion V4.5 Full or Curated unless the user names another model. V4.5 is the primary target. Circlestoneanima and Krea 2 may be similar enough for a cautious adaptation, while older SDXL models require a separate ordering and weighting strategy.

Never output artist strings, quality tags, score tags, or other quality boilerplate. Do not add them even when the user supplies examples containing them. Preserve user-provided content only when it is relevant to the requested shot and does not violate this contract.

Treat this v1 as a pure prompt-writing skill. Do not operate ComfyUI, call image-generation APIs, edit image metadata, or create an automatic paste/export workflow.

## Input handling

Accept any combination of:

- character baseline tags and prompt fragments;
- a natural-language description of the target shot;
- completed tag strings supplied as references;
- storyboard, previous-shot, or next-shot context.

Use exactly the supplied materials. If an item is absent, omit it or ask one focused clarification when it is necessary for a stable result. Do not fabricate a tag by translating an arbitrary Chinese word into English.

Do not silently add artist names, quality terms, negative-prompt boilerplate, LoRA identifiers, model metadata, or unverified Danbooru tags. If a supplied reference contains any of these, exclude them from the copyable prompt and mention the omission briefly only when useful.

For unknown, ambiguous, or model-specific tags, preserve the user's spelling and mark uncertainty in a short note after the prompt. Do not claim that an unverified rule is official NovelAI documentation.

## Workflow

### 1. Parse the shot

Extract only the facts needed for the current frame:

- framing and distance: establishing shot, full body, cowboy shot, medium shot, close-up, extreme close-up, or another precise user request;
- camera angle and view: eye-level, low angle, high angle, from above, from below, front view, side view, back view, three-quarter view, looking at viewer, looking away;
- composition: subject count and placement, facing direction, head direction, gaze direction, interaction relationships, and visible crop boundaries;
- environment: location, time, weather, lighting, background, and props that appear in or are touched within the frame;
- each character's visible clothing, accessories, hairstyle, facial expression, body traits, pose, action details, and interaction objects.

Use storyboard context to maintain continuity, but let the current shot override stale details.

### 2. Build a shot-specific inventory

Create a private inventory before writing the output. Classify each candidate item as `global`, `character-N`, `interaction`, or `out-of-frame`.

Delete `out-of-frame` details. For example, remove shoes, lower-body anatomy, and full-body pose details from an upper-body close-up unless they affect a visible interaction. Likewise remove distant environmental objects that cannot appear in the crop. Do not blindly carry a base prompt into a new shot.

Keep a reusable continuity base only as an internal reference. When the shot changes, regenerate the visible subset and revise both environment and character sections.

### 3. Choose vocabulary and order

Prefer common, established Danbooru tags when the concept has a known tag. Do not translate freely, coin tags, or turn a long sentence into a tag cloud. Use a short natural-language sentence only when it expresses a precise relation, staging constraint, or action that tags cannot express cleanly.

Order each prompt from high-impact to low-impact information:

1. shot-defining composition and camera;
2. essential subject count and placement;
3. major action or interaction;
4. character identity and visible appearance;
5. clothing and accessories visible in the crop;
6. facial expression, gaze, and fine pose details;
7. environment, lighting, and small props that remain visible.

Avoid repeating synonyms. Use one concise tag or phrase per fact. Put a fact earlier only when it must dominate; do not repeat it as fake emphasis.

### 4. Render the required output

Use this structure, adding or removing character blocks to match the scene:

```text
## Global scene prompt
`camera/framing, composition, environment, visible props, lighting, ...`

中文参考：……

## Character 1 prompt
`visible clothing, accessories, hairstyle, expression, face, body traits visible in crop, pose, action, gaze, head direction, interaction, ...`

中文参考：……

## Character 2 prompt
`...`

中文参考：……

## Self-check
- model target: NAI v4.5
- artist/quality tags excluded
- camera and crop are explicit
- out-of-frame details removed
- character count and interactions align
- order is deliberate and redundant phrases removed
```

Keep each English prompt in one copyable code span or code block. Put the Chinese translation directly below its corresponding prompt. The translation is for reference and must not be mixed into the copyable English prompt.

For a multi-shot request, first state a compact continuity base internally, then output each shot separately with its own fully revised global and character blocks. Do not output a single unchanged prompt reused across shots.

If the user asks for a reusable continuity base, keep it compact and separate from the shot outputs. Treat it as an internal planning reference unless the user explicitly asks to see it; every visible shot still needs its own revised prompts.

## Content boundary

Do not browse by default. Use an MCP or web search only when the user explicitly asks for external references or when a model-specific fact needs verification. Prefer a narrow official documentation page or repository metadata over broad searches. Do not clone, download, or inspect a repository merely because it appears in search results. Never copy source text, prompt libraries, private data, credentials, tokens, cookies, SSH keys, or session artifacts into this skill. Record only high-level workflow ideas and public repository URLs when they are genuinely useful.

## Model adaptation

Treat NAI v4.5 syntax and ordering as the default. Before adapting to another model, identify the requested model and state which parts may differ: tag vocabulary, weighting syntax, character separation, negative prompts, and prompt-order behavior. Do not silently apply V4.5-specific syntax to older SDXL.

When official documentation is unavailable or ambiguous, label the rule as a practical heuristic and keep the output conservative. The reference notes in [`references/model-notes.md`](references/model-notes.md) record the current scope and known boundaries; update them only with checked sources.
