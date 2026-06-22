# Web Animation Skills

> Web animation skills for Claude Code — GSAP, SVG, Lottie, micro-interactions, page transitions, and 60fps performance, installed straight into your agent.

## Install

```bash
npx skills add iart-ai/web-animation-skills
```

Works with Claude Code and 40+ agents.

## What's included

| Skill | What it does |
|---|---|
| [gsap-web](./gsap-web) | Code-driven web motion with GSAP — timelines, ScrollTrigger, SplitText, Flip, and Lenis smooth-scroll sync. |
| [performant-web-animation](./performant-web-animation) | Hit 60/120fps by animating only `transform`/`opacity` and killing layout thrash. |
| [page-transition-animation](./page-transition-animation) | Enter/exit page transitions in the Next.js App Router, plus the AnimatePresence exit fix. |
| [accessible-animation](./accessible-animation) | Tiered `prefers-reduced-motion` handling that degrades gracefully instead of nuking motion. |
| [micro-interaction](./micro-interaction) | Hover/press feedback, toggles, toasts, drawers, and list/layout motion with Framer Motion and CSS. |
| [svg-animation](./svg-animation) | Stroke draw-on, path morphing, motion-along-path, and animated icons/gradients/filters. |
| [lottie-animation](./lottie-animation) | Integrate, control, theme, and export Lottie/dotLottie across web, iOS, Android, and React Native. |
| [ascii-animation](./ascii-animation) | Generative ASCII fields and image/video/3D-to-ASCII for terminals, canvas, and Three.js. |

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
- performant-web-animation
- page-transition-animation
- accessible-animation
- micro-interaction
- svg-animation
- lottie-animation
- ascii-animation

## Topics

`web-animation` `gsap` `svg-animation` `lottie` `micro-interactions` `css-animation` `page-transitions` `accessibility` `claude-skill`

## License

MIT

---

Built by **[iart.ai](https://iart.ai)** — turn a prompt, CSV, or brand kit into controllable Motion Graphics MP4: exact text and numbers, brand-locked styling, one-click local edits, batch export from data.
