# Component API

Compact reference for AI agents and developers working on the Slidev deck.

Use these existing layouts and components before considering new design primitives. `slides.md` should be enough for content work; open Vue sources only when this API reference is insufficient.

## Layouts

### `cover`
- Uses `presentationInfo` from global frontmatter.
- Shows title, subtitle, and semester with `CoverLogo` and `CoverBackdrop`.
- Matches the FH/FEP presentation design. Authors appear on the separate `team` slide.

### `team`
- Uses `presentationInfo.authors` without changing the frontmatter schema.
- Shows names and initials in blue cards: three on top, two centered below.

### `chapter-intro`
- Expects per-slide `chapter` in frontmatter.
- Renders chapter progress with `ChapterOutline`.

### `default`
- Uses per-slide `title`, `subtitle`, `chapter`.
- Wraps content in `SlideLayout` (header, divider, footer, footnotes).

### `closing`
- Shows “Vielen Dank” and “Gibt es noch Fragen?” with `CoverLogo` and `CoverBackdrop`.

### `appendix-desktop`
- Default layout with centered single desktop-style visual.

### `appendix-mobile`
- Default layout with 3-column grid for mobile screenshots.

### `appendix-screenshots`
- Default layout with 2 columns (`Columns`).

## Components

### `BulletedList`
- Props: `title?: string`
- Slot: list items (`<li>` expected)

### `NumberedList`
- Props: `title?: string`, `size?: 'sm' | 'md'`, `start?: number`
- Slot: list items (`<li>` expected)

### `Text`
- Props: `title?: string`
- Slot: rich text content

### `SubText`
- Slot: secondary text line

### `HighlightedText`
- Props: `color?: string`, `weight?: string`
- Slot: inline highlighted content

### `DefinitionBox`
- Props: `title: string`, `source?: string`
- Slot: box content

### `ExampleBox`
- Props: `title: string`, `source?: string`
- Slot: box content

### `Quotebox`
- Props: `source?: string`
- Slot: quote text

### `Divider`
- Props: `length?: string | number`, `color?: string`, `thickness?: string`

### `Columns`
- Props: `columns?: string`, `gap?: string`
- Slot: column content

### `Image`
- Props:
  - `src: string` (required)
  - `title?: string`, `alt?: string`, `caption?: string`, `source?: string`
  - `width?: string`, `maxWidth?: string`, `height?: string`
  - `figureId?: string`
  - `captionAlign?: 'left' | 'center' | 'right'`
- Registers figure numbering when `caption` or `source` is set.

### `FigureList`
- Props: `title?: string` (default `Abbildungsverzeichnis`)
- Uses figures registered by `Image`.

### `Footnote`
- Props: `text: string` (required)
- Inline footnote marker; rendered in footer area by layout.

### `Table`
- Props:
  - `headers: any[]` (required)
  - `rows: any[]` (required)
  - `caption?: string`
  - `columnWidths?: string[]`
  - `size?: 'sm' | 'md' | 'lg'`
  - `accent?: 'blue' | 'gray'`
  - `highlights?: number[]`
- Supports `v-html` in cells.

### `CitationTable`
- Props: `title?: string`, `citations?: Array<{ id: string; text: string }>`, `idWidth?: string`
- Optional slot below table.

### `ChapterOutline`
- Props: `chapter: number` (required)
- Reads chapter labels from `presentationInfo.chapters`.

### `Outline`
- Slot: outline item components

### `OutlineItem`
- Props: `number: number | string`, `active?: boolean`, `disabled?: boolean`
- Slot: label text

### `NumberBadge`
- Props: `number: number | string`, `active?: boolean`, `disabled?: boolean`, `size?: 'sm' | 'md'`

### `SectionTitle`
- Props: `text?: string`
- Slot: title override

### `SlideLayout`
- Props: `title?: string`, `subtitle?: string`
- Slot: slide body

### `Todo`
- Props: `text?: string`

## Composables

### `useFigures`
- `registerFigure(uniqueId, figure)`
- `getFigures()`
- `clearFigures()`
- `hasFigure(uniqueId)`

### `provideFootnotes(slideContext)`
- Returns `{ register, footnotes }` for per-slide footnote handling.
