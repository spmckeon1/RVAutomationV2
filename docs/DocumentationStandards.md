# Documentation Standards

Defines the standards used when creating and maintaining project
documentation.

The goal of these standards is to ensure that project documentation is
consistent, readable, maintainable, and easy to navigate.

---

## General

- Documentation shall be written in Markdown.
- Documentation shall use UTF-8 encoding.
- Documentation files shall use LF line endings.
- Documentation shall be written in clear, concise English.
- Each document shall have a single, well-defined purpose.

---

## Document Structure

Each document shall begin with:

- Title
- Brief description of the document's purpose

Sections shall be organized logically and use Markdown headings.

---

## Headings

Use Markdown headings in hierarchical order.

Example:

# Title

## Major Section

### Subsection

#### Detail

Heading levels shall not be skipped.

---

## Diagrams

Documentation diagrams shall use plain ASCII characters only.

Reasons include:

- Portable across operating systems.
- Readable in terminal editors.
- Compatible with Git source control.
- Avoid Unicode font and encoding issues.
- Easy to edit without specialized tools.

Preferred diagram elements include:

    +----------------------+
    |                      |
    +----------------------+

            |
            V

    +--------+--------+
    |                 |

---

## Figures

Diagrams and illustrations should be accompanied by a descriptive
caption.

Example:

Figure 1. Logging Service Data Flow

---

## Code Examples

Code examples shall be enclosed in fenced Markdown code blocks.

The language identifier should be included whenever practical.

Example:

```javascript
function example() {
    return true;
}
```

---

## Tables

Markdown tables should be used when presenting structured reference
information.

---

## Maintenance

Documentation shall be updated as part of the change that introduces or
modifies the documented behavior.