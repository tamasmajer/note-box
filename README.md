# NoteBox Markup

The simplest text markup for personal notes and journals. 

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

Links do not need to be tags, you can simply add http://.. to the end of a line where it does not bother anybody. They are easy to find, and they should not be long anyway. 

You could use markdown-like links but separated with space like [link] (http://) to avoid markdown collision. Could reference images the same way. Or quoted "link" (http://).

Markdown has embedded sections which we do not, so just put the subsections below and reference them from the parent section like `-> [subsection]`:
```
[Summary]:
Main content here
-> [Details]
-> [More Info]
```

You can use a line containing only `:` to connect paragraphs or other content to create a single block, instead of concatenating them directly:
```
[Notes]:
First paragraph
:
Second paragraph
:
Third paragraph
```

For emphasis without brackets, you could use quotes, like 'italic' or "bold" in markdown.


## Parsing

```regex
Section:    ^---$
Block:      \n\s*\n    # split at blank lines
Entry:      (?:^|\n\s*\n)\[([a-zA-Z0-9 _.\-:/]+)\](?:\s*\[[a-zA-Z0-9 _.\-:/]+\])*\s*$    # allow multiple tags
Tag:        (?:^|\W)\[([a-zA-Z0-9 _.\-:/]+)\]    # limit contents to prevent conflicts
Link:       https?:\/\/[^\s<>\"]+
```

## Why?

- It is the laziest way I know to create structure in brain dumps.
- One file can last very long, searchable, local, safe, always open, no need to remember where to find it.
- Blocks are quotable, reusable, context independent.
- Tags are lazy, they are basically just highlights for easy skimming.
- Chronologic order, keep past journal entries as they are, but instead copy and meld their blocks into a new block.
- Could create interesting views, like a concept wiki, or a current view (with the most recent or pinned ones on top), bookmarks view, etc.
- I tried using other systems but I just keep coming back to this.
- So it is worth the effort to explore whether it can evolve any further.

