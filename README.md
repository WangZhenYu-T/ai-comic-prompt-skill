# AI Comic Prompt Skill

An extensible collection of skills for AI-assisted comic production.

The first release is a pure prompt-writing skill for NovelAI Diffusion V4.5. It converts storyboards, scene descriptions, character references, and existing tag strings into concise, shot-aware prompts organized by global scene and character. It preserves the requested model-specific workflow, prompt ordering, crop-aware detail selection, and Chinese reference translations.

The repository is designed to grow as separate skills are added under [`skills/`](skills/):

- [`skills/nai-v45-comic-prompt/`](skills/nai-v45-comic-prompt/): current NovelAI Diffusion V4.5 prompt assistant.
- A future ComfyUI MCP skill: allow an agent to pass approved prompts into ComfyUI, run workflows, inspect results, and iterate on generations.
- Future production-tool skills: connect the agent to Photoshop or other image-editing and manga-layout tools for cleanup, lettering, panel composition, and final export.

The long-term direction is an agent-driven, one-stop AI comic production workflow. Each model or production tool can remain an independent skill with its own instructions and integration boundary, while later orchestration skills coordinate them.

## Current scope

Version 1 is intentionally limited to prompt writing. It does not call image-generation APIs, operate ComfyUI, edit image metadata, control Photoshop, or automate clipboard actions.

The current skill targets NovelAI Diffusion V4.5 Full and Curated. Other model-specific prompt skills can be added as separate subdirectories rather than changing the V4.5 skill's contract.

## Roadmap

- **v1:** pure NovelAI V4.5 prompt-writing skill.
- **v2:** optional MUV-style front-end constraints and structured prompt validation for more consistent inputs and outputs.
- **Later:** ComfyUI MCP execution, result inspection and iteration, Photoshop or image-editing integration, manga panel layout, lettering, and end-to-end orchestration.

## Skill layout

Each skill should be self-contained:

```text
skills/
└── <skill-name>/
    ├── SKILL.md
    ├── agents/openai.yaml
    └── references/
```

Keep model-specific rules and tool-specific integration instructions in their own subdirectories. Shared orchestration should be introduced only when the related skills and MCP interfaces are ready.
