# 60fps Web Animation

Eliminate janky web animation by animating only the properties the browser can composite cheaply. For frontend developers fixing stutter, dropped frames, and layout thrashing — mapping expensive `width`/`top`/`box-shadow` animations to GPU-friendly `transform` and `opacity` for smooth 60/120fps motion.

## When it activates

- "Fix janky CSS animation" or "make animation 60fps"
- "Stop layout thrashing" or "animate width/height/top/left smoothly"
- "Convert animation to transform", "animate box-shadow performantly", or "animate height auto"
- "FLIP animation" or "why is my scroll/hover animation choppy"

## Example prompts

- "My CSS animation is janky — make it run at 60fps."
- "How do I animate height: auto smoothly with FLIP?"
- "Convert this top/left animation to use transforms."

## What's inside

- `SKILL.md` — the layout → paint → composite model and the expensive-to-cheap property map
- `references/patterns-and-profiling.md` — animation patterns and how to profile for jank

---
Part of **[Web Animation Skills](../)** · Built by **[iart.ai](https://iart.ai)** — controllable Motion Graphics MP4 from a prompt or data.
