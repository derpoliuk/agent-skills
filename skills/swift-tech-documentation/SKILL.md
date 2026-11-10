---
name: swift-tech-documentation
description: >-
  Guidance for writing and reviewing technical documentation in Swift repositories, including READMEs, repository docs, architecture decision records (ADRs), and documentation and implementation comments. Use when creating or reviewing Swift project docs, choosing where documentation belongs, or documenting Swift APIs.
---

# Swift Tech Documentation

This skill covers technical documentation: how a system works and why important choices were made. Functional requirements belong with the product or work planning process. Before writing, check the repository's existing conventions for file headers, documentation locations, templates, and references. Follow those conventions where they apply.

## Principles

- Explain information a reader cannot readily infer from the code. Avoid repeating names or restating operations.
- Keep each fact in one place and link to it elsewhere.
- Put details near the code they explain. Use broader documents for concepts that span files or components.
- Update documentation in the same change as the behavior it describes.
- Describe the current state in READMEs and repository documentation. Don't point to planned work, open pull requests, or follow-up issues ("not yet", "until then", "comes with #42"). A follow-up may never land, but the reference stays and the document goes out of date. State a known gap as a current fact: "Responses aren't cached; each request goes to the network." Plans belong in the change description, a pull request comment, or an ADR when a change spans several pull requests. Code comments follow their own rules (see "Implementation comments").
- If an API is hard to describe simply, consider whether its design can be clearer.
- Comments support abstraction: callers should not need to read an implementation to learn how to use an API. Tests verify behavior but do not replace usage documentation.

## Choose a location

- Express constraints in names, types, and code when possible. Put explanations of local behavior or trade-offs beside the relevant code.
- Use a README for what a repository or component does and how to build, run, and use it.
- Use repository documentation for concepts spanning multiple files or components.
- Use an ADR for a significant architectural decision and its rationale.
- Summarize relevant context in code or repository documentation when it would otherwise exist only in a discussion or work item.

For new Swift files, copy the file header pattern from neighboring files when one exists. Do not invent an author, date, organization, or target name. If neighboring files have no header, do not add one solely because of this skill.

## Swift documentation comments

- Write `///` documentation comments for public and internal declarations. Private declarations are optional, but document them when their usage contract is not clear. Follow any different local convention where the repository requires it.
- Describe what a type represents and how callers use it. For a property, clarify meaning, units, valid range, or when a value is `nil` if the type does not make that clear.
- For a documented function, explain every parameter, its return value, and thrown errors where applicable. Include side effects, preconditions, and threading requirements when callers need them. Apply the same standard to a private function once you choose to document it.
- Use words that add meaning beyond the declaration's name and signature. Avoid comments such as `- Parameter value: The value.`
- After a summary and any discussion, list Swift documentation callouts in this order: `- Parameter` or `- Parameters`, then `- Throws`, then `- Returns`. Use `- Parameter name:` for one parameter and a `- Parameters:` list for several.

```swift
/// Returns the title to display for an item.
///
/// - Parameter item: The item whose display title is needed.
/// - Returns: A trimmed title, or a fallback when the item has no title.
func displayTitle(for item: Item) -> String
```

## Implementation comments

- Explain why non-obvious code is necessary, especially timing, ordering, workarounds, and dependencies across components. Prefer clearer code over a comment that compensates for an unclear name or structure.
- Comment reactive operators such as Combine's `dropFirst`, `prefix`, `debounce`, `throttle`, and `delay` when their purpose is not clear from surrounding code. Explain the behavior being avoided or required, not the operator's definition.
- Put the reason for a workaround next to it. Include a work-item reference when one exists and the repository's conventions call for it; do not invent one.
- Describe unfinished work specifically. Follow the repository's existing format for TODOs.
- Avoid narration such as `// Increment counter`. A useful comment explains a constraint:

```swift
publisher
    .dropFirst() // Ignore the initial value; refresh only after a change.
    .sink { value in
        refreshView(for: value)
    }
```

## Architecture decision records

When creating, reviewing, or updating an ADR, read [references/adrs.md](references/adrs.md) for the template and lifecycle rules. Load this reference only when the task involves an architectural decision record.

## Writing style

- Use ATX headings and fenced code blocks with a language tag.
- Write one paragraph per line; let the editor wrap it.
- Use lists for parallel items and prose for connected reasoning.
- Use bold only for a short phrase a skimming reader must notice. Headings and list structure already provide emphasis; use italics for lighter emphasis.
- Use reference-style links when a URL appears more than once.
- Match any existing repository Markdown conventions.
