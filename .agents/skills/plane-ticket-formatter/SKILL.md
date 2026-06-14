---
name: plane-ticket-formatter
description: Guides agents on how to construct and format Plane.so work item descriptions and comments using Tiptap-compatible HTML.
---

# Skill: Plane Ticket Formatter

Use this skill whenever you need to create or update work items or comments in Plane.so with structured or rich text formatting. This skill provides the exact HTML structures required by Plane's ProseMirror/Tiptap-based editor.

---

## 0. Token Optimization Strategies

*   **HTML Simplification (Semantic HTML)**: Although Plane's internal editor uses verbose class names (`class="editor-paragraph-block"`) and block-level UUIDs (`data-id="..."`), Plane's backend parses standard semantic HTML automatically.
    *   *For basic tickets*: Send clean, minimal HTML (e.g., `<h1>Heading</h1>`, `<p>text</p>`, `<ul><li>item</li></ul>`). This is much shorter and saves a substantial amount of tokens.
    *   *For complex/interactive tickets*: Only include the strict Tiptap formatting tags and classes when utilizing specialized, interactive nodes (e.g., custom callouts, checkboxes, or user mentions).

---

## 1. Description HTML Formatting Template

When creating or updating a work item, pass the HTML representation in the `description_html` field. For best results, use unique UUIDs for all `data-id` and `id` attributes.

Below is the complete reference HTML template showing all supported formatting elements:

```html
<!-- Headings (H1 to H6) -->
<h1 class="editor-heading-block" data-id="UUID-1">Heading 1 🚀</h1>
<h2 class="editor-heading-block" data-id="UUID-2">Heading 2</h2>
<h3 class="editor-heading-block" data-id="UUID-3">Heading 3</h3>
<h4 class="editor-heading-block" data-id="UUID-4">Heading 4</h4>
<h5 class="editor-heading-block" data-id="UUID-5">Heading 5</h5>
<h6 class="editor-heading-block" data-id="UUID-6">Heading 6</h6>

<!-- Paragraph with standard text -->
<p class="editor-paragraph-block" data-id="UUID-7">
  <span>This is standard paragraph text. Plane supports inline formatting: </span>
  <strong><span>bold</span></strong>, 
  <em><span>italicized</span></em>, 
  <u><span>underlined</span></u>, and 
  <s><span>strikethrough</span></s>.
</p>

<!-- Horizontal Rule (Divider) -->
<div class="py-4 border-strong-1" data-id="UUID-8" data-type="horizontalRule"><div></div></div>

<!-- Numbered List -->
<ol class="list-decimal pl-7 space-y-(--list-spacing-y) tight" data-id="UUID-9" data-tight="true">
  <li class="not-prose space-y-2" data-id="UUID-10">
    <p class="editor-paragraph-block" data-id="UUID-11">First numbered list item</p>
  </li>
  <li class="not-prose space-y-2" data-id="UUID-12">
    <p class="editor-paragraph-block" data-id="UUID-13">Second numbered list item</p>
  </li>
</ol>

<!-- Bullet List -->
<ul class="list-disc pl-7 space-y-(--list-spacing-y) tight" data-id="UUID-14" data-tight="true">
  <li class="not-prose space-y-2" data-id="UUID-15">
    <p class="editor-paragraph-block" data-id="UUID-16">First bullet list item</p>
  </li>
  <li class="not-prose space-y-2" data-id="UUID-17">
    <p class="editor-paragraph-block" data-id="UUID-18">Second bullet list item</p>
  </li>
</ul>

<!-- Task/Todo List (Checkboxes) -->
<ul class="not-prose pl-2 space-y-2" data-id="UUID-19" data-type="taskList">
  <li class="relative" data-id="UUID-20" data-checked="true" data-type="taskItem">
    <label><input type="checkbox" checked="checked"><span></span></label>
    <div><p class="editor-paragraph-block" data-id="UUID-21">Completed checklist task</p></div>
  </li>
  <li class="relative" data-id="UUID-22" data-checked="false" data-type="taskItem">
    <label><input type="checkbox"><span></span></label>
    <div><p class="editor-paragraph-block" data-id="UUID-23">Pending checklist task</p></div>
  </li>
</ul>

<!-- Blockquote -->
<blockquote data-id="UUID-24">
  <p class="editor-paragraph-block" data-id="UUID-25">This is a blockquote for emphasizing text or quoting external sources.</p>
</blockquote>

<!-- Code Block -->
<pre class="" data-id="UUID-26"><code>def greet():
    print("Code block formatted natively!")</code></pre>

<!-- Table -->
<table data-id="UUID-27">
  <tbody>
    <tr style="">
      <th colspan="1" rowspan="1" colwidth="200" background="none" style="">
        <p class="editor-paragraph-block" data-id="UUID-28">Header Column 1</p>
      </th>
      <th colspan="1" rowspan="1" colwidth="200" background="none" style="">
        <p class="editor-paragraph-block" data-id="UUID-29">Header Column 2</p>
      </th>
    </tr>
    <tr style="">
      <th colspan="1" rowspan="1" colwidth="200" background="none" style="">
        <p class="editor-paragraph-block" data-id="UUID-30">Row Header</p>
      </th>
      <td colspan="1" rowspan="1" colwidth="200" style="">
        <p class="editor-paragraph-block" data-id="UUID-31">Normal cell</p>
      </td>
    </tr>
    <tr style="">
      <th colspan="1" rowspan="1" colwidth="200" background="none" style="">
        <p class="editor-paragraph-block" data-id="UUID-32">Row Header</p>
      </th>
      <td colspan="1" rowspan="1" colwidth="200" background="var(--editor-colors-pink-background)" style="background-color: var(--editor-colors-pink-background);">
        <p class="editor-paragraph-block" data-id="UUID-33">Pink background cell</p>
      </td>
    </tr>
  </tbody>
</table>

<!-- Callouts -->
<!-- Default Callout (Gray background, lightbulb emoji) -->
<div data-id="UUID-34" id="UUID-35" data-emoji-unicode="128161" data-emoji-url="https://cdn.jsdelivr.net/npm/emoji-datasource-apple/img/apple/64/1f4a1.png" data-logo-in-use="emoji" data-background="" data-block-type="callout-component">
  <p class="editor-paragraph-block" data-id="UUID-36">Callout default (gray background) with a <span>💡</span> emoji.</p>
</div>

<!-- Custom Callout (Green background, halo emoji, nested quote and code block) -->
<div data-id="UUID-37" id="UUID-38" data-emoji-unicode="128519" data-emoji-url="https://cdn.jsdelivr.net/npm/emoji-datasource-apple/img/apple/64/1f4a1.png" data-logo-in-use="emoji" data-background="green" data-block-type="callout-component">
  <p class="editor-paragraph-block" data-id="UUID-39">Green background callout with an <span>😇</span> emoji containing nested formats:</p>
  <pre class="" data-id="UUID-40"><code>Nested code block in callout</code></pre>
  <blockquote data-id="UUID-41">
    <p class="editor-paragraph-block" data-id="UUID-42">Nested blockquote in callout</p>
  </blockquote>
</div>

<!-- Text Alignments and Custom Colors -->
<p class="editor-paragraph-block" data-id="UUID-43">
  <span data-text-color="peach" data-background-color="green">Peach text on a green background.</span>
</p>
<p class="editor-paragraph-block" data-id="UUID-44" style="text-align: right;">
  <strong><span data-text-color="peach" data-background-color="dark-blue">Right-justified text.</span></strong>
</p>
<p class="editor-paragraph-block" data-id="UUID-45" style="text-align: center;">
  <span>Center-justified text.</span>
</p>

<!-- Mentions and External Links -->
<p class="editor-paragraph-block" data-id="UUID-46">
  <span>Mentioning a user: </span>
  <mention-component id="UUID-47" entity_identifier="USER-UUID" entity_name="user_mention"></mention-component>
  <span> and linking to a website: </span>
  <a target="_blank" class="text-accent-secondary underline underline-offset-[3px] hover:text-accent-primary transition-colors cursor-pointer" href="https://plane.so" rel="noopener noreferrer">Plane Website</a>.
</p>
```

---

## 2. Comment HTML Formatting Template

Work item comments can be added using `comment_html`. They support the same rich-text structures as work item descriptions.

Here is a standard formatted comment template:

```html
<h3 class="editor-heading-block" data-id="UUID-C1">Comment Title</h3>
<p class="editor-paragraph-block" data-id="UUID-C2">Feedback on ticket progress:</p>
<ul class="list-disc pl-7 space-y-(--list-spacing-y) tight" data-id="UUID-C3" data-tight="true">
  <li class="not-prose space-y-2" data-id="UUID-C4">
    <p class="editor-paragraph-block" data-id="UUID-C5">Item with <code>inline code</code> block.</p>
  </li>
  <li class="not-prose space-y-2" data-id="UUID-C6">
    <p class="editor-paragraph-block" data-id="UUID-C7">Mentioning <mention-component id="UUID-C8" entity_identifier="USER-UUID" entity_name="user_mention"></mention-component> to notify them.</p>
  </li>
</ul>
```

---

## 3. Formatting Gotchas & Guidelines

*   **Generate Unique UUIDs**: Plane uses block-level editing. Every heading, paragraph, list, list item, blockquote, table, and callout should have a unique `data-id` (and `id` for components that support it, like callouts) in UUIDv4 format. If editing programmatically, run a script to dynamically generate these.
*   **Color Values**: Custom text colors and background colors are handled via `data-text-color` and `data-background-color` attributes. Valid colors include standard design tokens like `"peach"`, `"green"`, `"dark-blue"`.
*   **Sanitization & Dangerous Tags**: Raw HTML strings are sanitized. Dangerous tags like `<script>` and `<iframe>` are completely stripped from the output.
*   **API Markdown Rendering Limitations**: Unlike the frontend interface, the Plane REST API does NOT convert raw Markdown (like `# Heading`) to HTML tags dynamically. While simple styling like bold/italics/bullets might be rendered in the browser under some conditions, headers (`#`) and complex structures will fail. Always construct and send valid HTML.
*   **Plain Text Mentions vs Native Badges**: Plain text mentions (e.g. `@Username` or `@UUID`) sent via the API are NOT resolved. You must use the `<mention-component>` tag with the user's exact UUID to render native mention badges.
*   **Auto-linking**: Raw URL strings (e.g. `https://plane.so`) are not automatically wrapped in HTML anchors by the API. Always use explicit `<a>` tags.
*   **Clearing Descriptions/Comments**: Sending an empty string `""` to `description_html` results in an **HTTP 400 Bad Request**. To clear a description or comment, send an empty wrapper like `<div></div>` or `null`.
*   **Plain Text Stripping**: Always populate `description_stripped` (for tasks) or `comment_stripped` (for comments) with a plain text version of the content to prevent display glitches in search views and mail digests.
