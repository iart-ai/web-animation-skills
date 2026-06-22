# Web Animation Skills

> Web animation skills for AI coding agents — GSAP, SVG, Lottie, micro-interactions, page transitions, and 60fps performance, installed straight into your agent.

![Web Animation Skills — animated showcase](./showcase.gif)

## Install

```bash
npx skills add iart-ai/web-animation-skills
```

Or add it as a Claude Code plugin marketplace:

```bash
/plugin marketplace add iart-ai/web-animation-skills
```

then `/plugin install web-animation-skills`.

Works with Claude Code, Cursor, Codex, GitHub Copilot, and 40+ agents.

## What's included

| Skill | What it does |
|---|---|
| [gsap-web](./skills/gsap-web) | Code-driven web motion with GSAP — timelines, ScrollTrigger, SplitText, Flip, and Lenis smooth-scroll sync. |
| [60fps-animation](./skills/60fps-animation) | Hit 60/120fps by animating only `transform`/`opacity` and killing layout thrash. |
| [page-transition-animation](./skills/page-transition-animation) | Enter/exit page transitions in the Next.js App Router, plus the AnimatePresence exit fix. |
| [accessible-animation](./skills/accessible-animation) | Tiered `prefers-reduced-motion` handling that degrades gracefully instead of nuking motion. |
| [micro-interaction](./skills/micro-interaction) | Hover/press feedback, toggles, toasts, drawers, and list/layout motion with Framer Motion and CSS. |
| [glassmorphism](./skills/glassmorphism) | Frosted-glass / Apple "Liquid Glass" UI — backdrop-filter panels, edge highlights, refraction, and animated specular sweeps, with reduced-transparency fallbacks. |
| [svg-animation](./skills/svg-animation) | Stroke draw-on, path morphing, motion-along-path, and animated icons/gradients/filters. |
| [lottie-animation](./skills/lottie-animation) | Integrate, control, theme, and export Lottie/dotLottie across web, iOS, Android, and React Native. |
| [ascii-animation](./skills/ascii-animation) | Generative ASCII fields and image/video/3D-to-ASCII for terminals, canvas, and Three.js. |

## When it activates

- You ask Claude to build scroll-driven, hero, or text-reveal animations on the web
- A CSS, hover, or scroll animation feels janky and you want smooth 60fps
- You need animated page/route transitions in Next.js
- You want UI micro-interactions, SVG motion, Lottie playback, or ASCII effects
- You need animation that respects reduced-motion and WCAG

## Example prompts

- "Build a pinned hero section that scrubs a timeline to scroll with GSAP."
- "My CSS animation is janky — make it run at 60fps."
- "Add page transitions in my Next.js App Router app; the exit animation never fires."
- "Make my animations respect prefers-reduced-motion without removing everything."
- "Animate this SVG logo to draw itself on."

## Skills

- gsap-web
- 60fps-animation
- page-transition-animation
- accessible-animation
- micro-interaction
- glassmorphism
- svg-animation
- lottie-animation
- ascii-animation

## Topics

`web-animation` `gsap` `glassmorphism` `svg-animation` `lottie` `micro-interactions` `css-animation` `page-transitions` `accessibility` `claude-skill`

## More packs

Part of a 14-pack open-source collection — install only what you need. Full hub: **[github.com/iart-ai](https://github.com/iart-ai)**

[tiktok-video-skills](https://github.com/iart-ai/tiktok-video-skills) (TikTok / Reels / Shorts) · [text-message-video-skills](https://github.com/iart-ai/text-message-video-skills) (Text-message stories) · [youtube-video-skills](https://github.com/iart-ai/youtube-video-skills) (Podcasters & YouTubers) · [ecommerce-video-skills](https://github.com/iart-ai/ecommerce-video-skills) (E-commerce sellers) · [ad-video-skills](https://github.com/iart-ai/ad-video-skills) (Brand advertisers) · [data-animation-skills](https://github.com/iart-ai/data-animation-skills) (Analysts & PMs) · [explainer-video-skills](https://github.com/iart-ai/explainer-video-skills) (Educators) · [map-animation-skills](https://github.com/iart-ai/map-animation-skills) (Vox-style maps) · [motion-design-skills](https://github.com/iart-ai/motion-design-skills) (Motion designers) · [kinetic-typography-skills](https://github.com/iart-ai/kinetic-typography-skills) (Kinetic type / text) · [freelance-motion-skills](https://github.com/iart-ai/freelance-motion-skills) (Freelancers & studios) · [webgl-animation-skills](https://github.com/iart-ai/webgl-animation-skills) (3D / WebGL) · [manim-skills](https://github.com/iart-ai/manim-skills) (Math / educational)


## License

MIT

---

Built by **[iart.ai](https://iart.ai)** — the AI motion agent: describe it in a prompt — or point it at a CSV or brand kit — and get editable, on-brand motion graphics with exact text and numbers, one-click edits, and batch export.
