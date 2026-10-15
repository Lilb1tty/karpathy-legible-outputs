# legible-outputs

A Claude skill that picks the output format that makes a topic easiest to understand, instead of defaulting to dense prose.

It works up a ladder of formats:

1. Plain controlled writing in the style of ASD-STE100 (Simplified Technical English)
2. Diagrams
3. Interactive HTML pages
4. Narrated explainer videos (3Blue1Brown style)

## Install

Copy `SKILL.md` into a folder named `legible-outputs` in your skills directory, or upload the packaged `.skill` file in Claude.

## Why

As models do more of the work on their own, the person's job moves toward oversight and understanding. Richer formats lower the cost of reading and checking what a model produced.
