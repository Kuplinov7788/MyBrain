---
type: reusable-workflow
updated: 2026-09-23
---

# Remotion JS Infographic Workflow

Use when an original, educational JavaScript PNG infographic is needed through Remotion.

## Output standard

- Format: `1080×1080` PNG.
- Keep every idea in its own visually distinct card, label, or code section.
- Explain the learner’s actual questions, not only syntax: what it is, why it is used, and one real-project use case.
- Use a working JavaScript example. Avoid pseudo-code unless it is explicitly marked.
- Make the piece original; use a reference only for high-level visual direction, never copy its artwork or text.

## Content structure

1. Header: JavaScript tag, topic, and a plain-language one-line definition.
2. “Nima uchun ishlatiladi?” card: one purpose in everyday Uzbek.
3. “Natija” card: show the visible result of the code.
4. “Real project” code panel: use a recognisable data example such as `products`, API items, or a task list.
5. Data flow: input collection → loop → UI/result.
6. Closing takeaway: describe why the approach remains useful when the list length changes.

For a `for` loop, a good example is rendering a product card for every item in a `products` array. Include the resulting items in the visual so the relationship is obvious.

## Design system v1

- Canvas: `1080×1080`, outer padding `56px`, and a consistent 24px spacing rhythm.
- Deep navy background; near-white primary text; cool light-blue secondary text.
- Cyan marks data, purple marks loop/process, green marks output, and amber marks warnings or tips.
- Use a near-black monospace code panel and keep one idea per card.
- Maintain the hierarchy: title → definition → purpose → code → result → real project → FISHKA.
- Keep the bottom 10% quiet so the explanation remains the visual focus.

## Visual rules

- Use dark blue background, high-contrast code colours, and 2–4 accent colours.
- Reserve a distinct colour for each concept where it helps scanning: data, loop, and output.
- Do not overload the canvas. Prefer short lines and hierarchy over dense paragraphs.
- Use arrows or small chips to show the input → process → output sequence.
- Confirm text fits the canvas and is legible at phone size.

## Remotion execution

1. Read the existing composition before changing it.
2. Keep the project and output paths inside the trusted Remotion workspace.
3. Call `remotion_validate_js` with the exact educational snippet and expected output; do not render when syntax or output validation fails.
4. Run composition discovery after edits; bundling must complete and list the intended composition.
5. Render the still via the trusted Remotion MCP tool.
6. Call `remotion_check_still` on the exact output path: format must be PNG, dimensions must be `1080×1080`, size must be within the limit, and the path must stay trusted.
7. Only return the exact artifact path reported by the render tool.
8. A local render is not proof of Telegram delivery. When the owner requests the result in the current chat, use `render_media` with that exact trusted output path.
9. Put the requested explanation in the Telegram caption below the image, with clear spacing and useful examples/results; do not send only a generic title. Keep it concise enough for Telegram’s 1024-character caption limit.

## Feedback loop

- The next owner message after delivery is feedback on the latest artifact.
- Classify feedback as content, design, readability, or technical before changing the composition.
- Keep approved parts and change only the requested issue.
- Save a new version (`v2`, `v3`, etc.) instead of overwriting an approved artifact.
- Send the new version to the current chat when requested and use approval as the next baseline.

## Verified example

The `ForLoopCard` composition in `/Users/protochka/.codex/remotion-workspace/demo` rendered an educational for-loop infographic with a real product-card example to:

`/Users/protochka/.codex/remotion-workspace/outputs/for-loop-card-v3.png`

The artifact was verified as PNG, `1080×1080`.
