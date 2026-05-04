# Switcher UI Spec (Reference-Matched)

## Visual extraction from provided images
- Segmented control on light neutral bar.
- 3 tabs: `Chat`, `Code`, `Cowork`.
- Selected tab (`Cowork` in reference) appears raised/light.
- Rounded corners on container and selected tab.
- Tight vertical sizing and compact typography.

## Layout metrics (approximate)
- Container height: 28–32px.
- Horizontal padding: 4–6px.
- Segment min width: 52–72px with centered label.
- Gap between segments: 0 (joined segmented control).
- Outer radius: ~8px; selected radius: ~6px.

## Typography feel
- Font size: ~12px.
- Weight: 500 active, 400 inactive.
- Color: medium-gray inactive; darker-gray active.

## States
- Default: neutral background, muted text.
- Hover: slight darkening of text and subtle bg tint.
- Active: white-ish fill with soft border and subtle shadow.
- Focus visible: 1–2px low-saturation ring.

## Motion
- Active state transitions should be quick and subtle (120–180ms).
- Use opacity/background-color/box-shadow transitions only.

## Accessibility
- Keyboard roving focus + Enter/Space activation.
- `aria-label="Mode switcher"`, each item `role="tab"`.
- Respect reduced motion preference.

## Implementation note
Implement in host frontend as reusable `Switcher` component with mode enum:
`chat | code | cowork`, controlled by orchestration context.
