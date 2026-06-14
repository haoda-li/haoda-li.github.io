# Notes Conversion

Use this skill when editing note files in the _notes folder and converting content to the distill-style format used by this site.

## When to use

Apply these conversions when a note contains:
- markdown image syntax such as ![alt](path)
- bibliography citations written as [@key]

## Conversion rules

### Images

Convert markdown images to the same figure include pattern used in the note templates.

Use this pattern:

```liquid
<div class="row mt-3">
    <div class="col-lg mt-3 mt-md-0">
        {% include figure.liquid path="assets/notes/your-image.jpg" class="img-fluid rounded z-depth-1" zoomable=true %}
    </div>
</div>
```

Rules:
- Replace markdown image syntax like ![alt](path) with the figure include block above.
- Use the correct asset path relative to the site root, for example assets/notes/file.jpg.
- Verify the target file exists in the assets folder before using it.
- Prefer the same style and spacing as the existing note files.

### Citations

Convert markdown-style citations to distill-compatible cite tags.

Replace:
- [@key] with <d-cite key="key" />
- Mixtral[@mixtral] with Mixtral <d-cite key="mixtral" />

### Front matter

When a note is missing or needs updated front matter:
- Use the first H1 heading as the title.
- Use the H2 headings as the TOC entries under toc -> name.
- Quote TOC names that contain special characters such as punctuation or parentheses.
- Remove the H1 heading from the markdown body once the title is already present in front matter.
- Keep the front matter consistent with the existing distill-style notes in _notes.

### Foldable blocks

Convert admonition-style foldable blocks of the form:

```md
??? some-label "title"
    content
```

to the details-style syntax:

```liquid
{% details title %}
content
{% enddetails %}
```

Rules:
- Use `???` as the main marker for the foldable block.
- Treat the token after `???` as a modifier or style label and ignore it for the conversion.
- Use the quoted title as the details label.
- Preserve the indented content as the body of the details block.
- Keep the surrounding markdown formatting intact.

### Include-style code snippets

Convert include-style code snippets of the form:

```md
```python
--8<-- "notes/research/scripts/file.py"
```
```

to:

```liquid
{% highlight python %}
{% include_relative scripts/file.py %}
{% endhighlight %}
```

Rules:
- Replace the fenced code block with a Liquid highlight block.
- Use the file path after `--8<--` to build the include_relative path.
- Strip the leading `notes/research/` prefix when converting to the site-relative include path.
- Preserve the original language tag as the highlight language.

## Notes

- These rules are intended for content in _notes and similar distill-style markdown notes.
- Keep the content readable and preserve the surrounding prose when converting.
- If a path does not exist, update it to the correct asset location or report the mismatch.
