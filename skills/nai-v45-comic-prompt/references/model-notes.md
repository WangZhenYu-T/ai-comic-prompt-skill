# Model notes

This skill targets NovelAI Diffusion V4.5 Full and Curated prompt writing. Keep this file conservative: it records scope and verified boundaries, not a complete tag dictionary.

## Current scope

- Use a mixture of common Danbooru-style tags and short natural-language control sentences.
- Treat prompt order as a practical priority mechanism: put shot-defining and composition-critical information first.
- Keep character and scene information separated so a user can paste or adapt them into a multi-character workflow.
- Remove details that the current crop cannot show. A continuity base is a planning aid, not a prompt that must be copied unchanged.
- Keep artist strings, quality tags, and score boilerplate outside the skill's output contract.

## Model boundaries

NAI v4.5 behavior, syntax, tag vocabulary, and weighting support are model-specific. Do not transfer these notes wholesale to older SDXL checkpoints. Circlestoneanima and Krea 2 may accept similar mixed tag and prose inputs, but their ordering, weighting, and tag behavior still require separate verification.

## Source policy

When a future revision needs external facts, prefer this order:

1. NovelAI's official documentation for model behavior and syntax.
2. Danbooru's tag pages for tag spelling and usage.
3. Directly relevant public repositories for workflow ideas, clearly marked as community practice.

Record the URL and access date in the commit message or an issue when adding a factual model rule. Do not copy large sections of another repository.

## Related public projects reviewed for structure

- `https://github.com/WeissGoat/nai45-prompt-skill`: a public V4.5 prompt skill with references, scripts, evals, and tests. Its repository metadata suggests that a larger future version may benefit from evaluation fixtures, but this v1 remains a pure instruction skill.
- `https://github.com/penguin045/nai-prompt-studio`: a browser-based V4.5 prompt studio. Its repository metadata suggests workflow ideas such as tag normalization, multi-character cards, and metadata reuse; this skill intentionally does not implement an editor.
- `https://github.com/tsukino4a/ComfyUI-4A-NovelAI`: a ComfyUI integration for V4.5+ with prompt scheduling and metadata handling. It is relevant to a later MCP or ComfyUI integration, not to this v1.

These projects were selected from repository-level search metadata only. Do not treat them as authoritative model documentation, and do not open their prompt or image content as part of normal skill use.
