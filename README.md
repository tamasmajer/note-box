# Text Tags

A simple text markup for personal notes and journals. 

Just write, then use brackets to highlight, add dates, tags, etc.

## Example

```
---
intro

[2025-09-29]
Today I worked on [project x] and met with [Alice].

[work]:
- Fixed bug in [module y]
- Started [feature z]

[personal]:
Went to gym. Read about [dopamine].

[2025-09-28]
Yesterday's notes here.

---
```

## Structure

```
File
└─ Section (separated by ---)
   └─ Entry (starts with a [tag] line)
      └─ Block (separated by blank lines)
```

Separate independent sections with `---`.

A blank line followed by a `[tag]` line creates a new entry.

Blocks are independent, quotable units with no blank lines inside.

A tag by itself creates a new entry, so add text to the same line to avoid starting a new entry (like `[sub]:`).

**Tags allow:** letters, numbers, spaces, `- _ . : /`

**Within a block, you could split the flow using patterns like:**
```
- Item
- [] Task
- [x] Done
-> Implies
=> Therefore
```

## Parsing

```regex
Section:    ^---$
Entry:      (?:^|\n\n+)\[([a-zA-Z0-9 _.\-:/]+)\]
Tag:        (?:^|\W)\[([a-zA-Z0-9 _.\-:/]+)\]
```
