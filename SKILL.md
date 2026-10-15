---
name: karpathy-legible-outputs
description: Choose and produce the output format that makes a topic easiest to understand and oversee, instead of defaulting to dense prose. Use whenever the user asks to explain, teach, walk through, summarize, or help them understand something (a codebase, an agent's behavior, a paper, a system, a concept, a model's output), or says an earlier answer was hard to read, too dense, or hard to follow. Also use when they ask for "ASD-STE100", "simple English", "a diagram", "an HTML explainer", "an interactive page", or "a 3b1b-style / explainer video". Make sure to use this skill even if they only say "help me understand X" or "explain this to me", because the right format matters as much as the content.
---

# Legible outputs

As models do more of the work autonomously, the person's job shifts toward oversight and understanding. The bottleneck is no longer producing output but reading it. This skill picks the format that lowers the cost of understanding, and builds it. Software artifacts are cheap now, so a custom, throwaway page or video is often worth making even for a one-off question.

## The ladder

Formats climb in richness. Each rung is usually easier to absorb than the one below, and costs more to make. Pick the rung that fits the topic, the stakes, and how long the person will spend with it.

1. **Plain controlled writing** (ASD-STE100 style). Default for short explanations.
2. **Diagram or image.** Use when the topic has structure: flows, hierarchies, timelines, comparisons, systems.
3. **HTML page.** Use when the topic benefits from layout, interaction, animation, toggles, step-throughs, or live parameters.
4. **Explainer video.** Use for concepts that unfold over time or need a narrated visual story. Heaviest option.

Move up the ladder when the content is spatial, sequential, quantitative, or something the person will revisit. Stay low when the question is small. A one-line answer does not need a video. If unsure, go one rung above the obvious choice and offer to go further.

## Rung 1: Controlled writing (ASD-STE100)

ASD-STE100 is Simplified Technical English, a controlled language built for aerospace maintenance manuals. Its constraints force clear writing. Apply the spirit of it:

- One idea per sentence. Keep sentences short (about 20 words for instructions, 25 for descriptions).
- Use simple verbs in the active voice. Prefer "Turn the valve" to "The valve should be turned".
- Use the same word for the same thing every time. Do not vary terms for style.
- Use one meaning per word. Avoid idioms, phrasal verbs, and figurative language.
- Put the instruction first, then the reason or condition.
- Use short paragraphs and clear steps for procedures. Put warnings before the step they apply to.
- Define a technical term once, then use it consistently.

The full spec is strict (approved word list, tense limits). Default to "80% of the way": follow the style rules above but allow needed technical vocabulary and natural phrasing. If the user asks for strict ASD-STE100, follow the spec as closely as you can and say where you had to deviate.

## Rung 2: Diagrams

A diagram is easier to parse than paragraphs when relationships matter. Choose the diagram type to match the content: flowchart for processes, sequence diagram for interactions over time, tree for hierarchy, table or matrix for comparison, plot for numbers. Keep labels short, limit to what the person needs, and add one or two sentences of text that say what to notice. Use the inline visual tools or an SVG/Mermaid file, whichever the session supports.

## Rung 3: HTML pages

Ask for or build the explanation as an HTML page when interaction helps: sliders that change a parameter, steppers that walk through an algorithm, collapsible detail, hover to reveal definitions, animation of a process. Build it as one self-contained file. Open with the one-paragraph takeaway, then let the person explore. Publish as an artifact when the session offers one (the person will likely keep or share it); otherwise write the `.html` file and send it. Make it work on a phone-width screen.

Design matters here. The goal is understanding, not decoration. Use motion only where it shows change over time or cause and effect.

## Rung 4: Explainer videos

For a 3Blue1Brown-style explainer, plan before building:

1. **Script first.** Write a short narration script (typically 2-5 minutes) with one idea per scene. Show it to the user if the topic is high-stakes or the video is costly to redo.
2. **Animate with code.** Manim is the usual tool for math and CS visuals (`pip install manim`). For other topics, build scenes with HTML/Canvas or matplotlib animations rendered to frames, then stitch with ffmpeg. Check what is installed before choosing.
3. **Narration audio.** If the user has an ElevenLabs API key, use it. If not, do not ask them to paste secrets into chat. Tell them where to set it as an environment variable, or use a free local text-to-speech option (for example Piper or Coqui TTS) that runs on local compute. Say which you used.
4. **Sync.** Time scenes to the narration length. Add captions as a fallback.
5. **Deliver** the `.mp4` and the script. Note how long it took and any limits (voice quality, missing fonts).

The sandbox may lack the network or compute for this. If rendering or audio fails, fall back one rung: deliver the script plus an HTML storyboard, and say what is missing.

## Choosing and communicating the choice

- If the user names a format, use it.
- If they do not, pick using the ladder, give the answer in that format, and add one line offering the next rung up ("I can turn this into an interactive page or a short explainer video").
- Always lead with a two-sentence plain summary, whatever the format. The richer formats support understanding; they should not hide the answer.
- Do not pad. A richer format is justified only when it makes the topic easier to understand or check.

## Why this works

Dense prose makes the reader do the parsing. Controlled language, visual structure, and interaction move that work from the person to the machine. For oversight tasks, such as reviewing what an agent did, this is more than polish: it is how a person stays able to catch mistakes.
