# MOSAIC

MOSAIC is a faceted life-management architecture for Obsidian. It brings together knowledge, journaling, projects, tasks, and other parts of everyday life in a single system while keeping capture simple and retrieval powerful.

The name comes from the idea of a mosaic: every note is a tile. Some tiles are small and atomic; others are larger and richer. Their size does not change their ability to participate in the larger picture. What matters is how they can be connected, described, filtered, and observed from different angles. The mosaic is the perspective that emerges when selected parts of your life are brought together in response to a particular question.

MOSAIC is ultimately less about where a note is stored than about how it can be observed.

Folders provide coarse operational structure.  
Entities define operational nature.  
Categories establish persistent contexts.  
Descriptors add lightweight facets.  
Tags mark exceptional transversal qualities.  
Links express relationships.  
Views recombine all of these dimensions into answers.

> **A mosaic is not a fixed representation of the vault. It is the perspective that emerges when the right tiles are selected and observed from the right angles for the question at hand.**


---

## Influences

MOSAIC is not a replacement for established knowledge-management methods. It combines ideas from [Tiago Forte's PARA method](https://fortelabs.com/blog/para/), **Zettelkasten**, and [Steph Ango's Obsidian vault](https://stephango.com/vault), while adapting them to a unique and flexible architecture.

### PARA

PARA inspires the coarse separation of the system into different operational areas.

- **Actions** contains active Projects and Tasks.
- **Nodes** contains the knowledge graph and other semantic notes.
- **Archive** contains material removed from the active working set.

The folder is therefore meaningful: it tells you the **role and lifecycle state of a note within the system**.

Projects and Tasks are grouped under `Actions/` because they belong to the same operational space and are fundamentally different from knowledge nodes. Keeping them physically separate also makes it easy to extract the action-management layer into a dedicated project-management vault in the future without restructuring the knowledge graph.

MOSAIC borrows PARA's operational separation without reproducing its folder taxonomy literally.

### Zettelkasten

Zettelkasten inspires the way knowledge can be developed inside `Nodes/`: notes should preferably be self-contained, written in your own words, and extensively connected through meaningful links.

MOSAIC deliberately keeps only this core idea. It does not require later Zettelkasten taxonomies such as **literature notes, permanent notes, fleeting notes**, or similar note classes.

Atomic notes are recommended, not mandatory. A small note is a small tile; a large, developed note is simply a larger tile. Both can still participate in the same mosaic through links and facets.

For this reason, MOSAIC is **compatible with Zettelkasten but does not require it**. The system adapts to the user's preferred note-taking style.

### Steph Ango's vault

Steph Ango's approach inspires MOSAIC in several ways:

- keeping the vault simple and allowing structure to emerge over time;
- using **Categories** as persistent perspectives backed by Obsidian Bases;
- relying on a common **Unique Note** entry point;
- using dated notes and reusable templates for personal journaling;

MOSAIC modifies these ideas by using a more explicit folder architecture and by decomposing classification into three independent layers: **Entity, Category, and Descriptor**.

This creates a faceted system in which notes can be retrieved from many angles without requiring a dedicated template and Base for every possible classification. Structure is formalized only when it becomes useful. Retrieval is made powerful, non-destructive and open to continuous changes.

---

## Vault structure

```text
Vault/
├── Actions/
├── Archive/
│	├── Actions/
│   ├── Calendar/
│	├── Nodes/
├── Attachments/
├── Calendar/
├── Inbox/
├── Journal/
├── Nodes/
├── Templates/
└── Views/
│   ├── Entities/
│   ├── Categories/
│   └── Custom/
```

### Folder semantics

`Attachments/` and `Templates` are supporting folders:
- `Attachments/` — non-Markdown assets.
- `Templates/` — reusable structures for notes.

All other folders express **state and/or role in the system**:
- `Actions/` — active Projects and Tasks, i.e. operational nodes.
- `Archive/` — material no longer part of the active system, such as very old meetings or completed projects.
- `Calendar/` — time related Events and Meetings.
- `Inbox/` — unprocessed notes. When notes are moved to other folders, they are considered processed nodes.
- `Journal/` — notes about the day. Makes memories over time.
- `Nodes/` — active knowledge nodes. Describe the world in the system.
- `Views/` — persistent Bases and saved perspectives over content.

### Graph view
Graph view is deliberately setup to filter out `Archive/`, `Templates/`, `Views/`, as well as the `README` file.

The corresponding filter is:
```
-path:"Archive" -path:"Templates" -path:"Views" -file:"README"
```

Remove the filter to visualize everything, or modify it according to your needs. You can consider to discard Actions and Calendar nodes as well.

---

## Workflow

The default entry point is **Unique Note**, which creates notes in `Inbox/`

Every new note starts from the same minimal template, which defines a minimal set of **properties**:

```yaml
created: "{{date:YYYY-MM-DD}}"
entity:
categories:
descriptors:
tags:
```

From there:
1. Assign the node **Entity**. For specialized entities, add the corresponding **template**.
2. Fill in additional properties.
3. Write the note body.

---

## Faceted organization

MOSAIC organizes notes through three primary semantic layers.

### Entity

The **Entity** defines the operational nature of the node: what kind of object it is in the system.

Typical Entities include:

- Concept: models a piece of knowledge.
- Item: models everything in the world outside of concepts, such as people, books, animals, etc.
- Journal: models daily personal and work memories.
- Project
- Task
- Meeting
- Event

A node has one primary Entity.

Entities are deliberately few. They exist only when different kinds of notes need meaningfully different behavior, role and structure.

> **Every Entity must have a corresponding Base in `Views/Entities/`.**

### Categories

**Categories are controlled contextual perimeters.**

They represent persistent macro-contexts such as:

- Finance
- Music
- Writing
- Software
- Personal
- Work

> [!tip] Work Category
> The Work category is extremely useful to separate between your personal life subjects and  work-related stuff.

A Category is important enough to deserve a permanent View. Therefore:

> **Every Category must have a corresponding Base in `Views/Categories/`.**

Categories should remain relatively stable, and widely used by nodes.

### Descriptors

**Descriptors are lightweight, free-form facets.**

They refine how a note can be found without changing its structure:

```yaml
descriptors:
  - option
  - volatility
  - pricing
```

Descriptors are intentionally cheap to create. They do not require a template, a Base, a hierarchy, or even long-term commitment. They can be added, removed, modified along time. Their order doesn't matter to research.

Categories and Descriptors may overlap semantically. The difference is their **importance and persistence**, not necessarily their vocabulary.

A recurring Descriptor can be promoted to a Category when it becomes useful as a permanent perspective over the vault.

> **Descriptors are created freely. Categories are promoted deliberately.**

Prefer singular terms in properties when practical. Views may use plural names because they represent collections.

---

## Linked Entities and Categories

Each Entity and Category is backed by a Base, so its property value should be stored as a link rather than plain text.

> [!warning] First reference and renaming
> Using bases as references is not ideal, since they carry the `.base` extension in the link. You may want to polish the link label. If that is the case, the first time you reference a base as an Entity/ Category from a note or template, you must write it by hand, and change the shown name, as described here below.

For example:

```yaml
entity: "[[Projects.base|Project]]"
```

The underlying file can use a plural collection name such as:

```text
Projects.base
```

while the alias keeps the semantic property clean:

```text
Project
```

The same convention applies to Categories:

```yaml
categories:
  - "[[Finance.base|Finance]]"
  - "[[Writing.base|Writing]]"
```

This makes metadata both **semantic and navigable**: clicking the property immediately opens the corresponding View.

Descriptors remain plain values because they are intentionally lightweight:

```yaml
descriptors:
  - option
  - volatility
  - pricing
```

---

## Tags

Tags are reserved for **exceptional transversal qualities**, not for domains, note types, or normal workflow state.

The initial MOSAIC vocabulary is intentionally small:

```text
#important
#inspiring
#memories
#review
#deprecated
#obsolete
```

- `#important` — unusually relevant or significant.
- `#inspiring` — something motivational, worth to remember.
- `#memories` — worth remembering for personal significance.
- `#review` — requires reviewing the content.
- `#deprecated` — still intelligible or usable, but no longer recommended as the current reference.
- `#obsolete` — superseded by time, facts, or a later version.

Tags belong to properties. It is discouraged to use tags in the body. Use them sparingly as an *exception*.

If a tag starts describing *what the note is about*, it should probably become a Category or Descriptor instead.

---

## Views, facets, and retrieval

Views are how MOSAIC turns metadata into perspectives.

Two kinds are automatic:

- `Views/Entities/` contains one Base for every Entity.
- `Views/Categories/` contains one Base for every Category.

`Views/Custom/` contains recurring questions that combine multiple facets, for example:

- open Finance Tasks;
- important Concepts about volatility;
- memorable Music Items;
- Projects with an upcoming deadline.

Descriptors do not require permanent Views. They can be retrieved ad hoc through Obsidian Search or Quick Switcher, and promoted into a Custom View only when the same question becomes recurring.

Examples of property searches:

```text
[descriptors:album]
[descriptors:"alternative rock"]
[categories:music] [descriptors:album]
[tags:important] [descriptors:volatility]
```

This is the core of MOSAIC: **notes remain cheap to create because classification is lightweight, while retrieval remains powerful because facets can be recombined according to the current question.**

The same tile can therefore appear in many different mosaics without being duplicated.

---

## Journaling

Journaling is treated as another use of the same node system rather than as a separate subsystem.

A Journal note starts from Unique Note and adds only the properties and structure specific to journaling:

```yaml
entity: "[[Journal.base|Journal]]"
date: "{{date:YYYY-MM-DD}}"
rating:
```

`created` records when the node was created, while `date` records the day the journal entry represents. This separation makes retroactive journaling possible.

A Journal template can then provide sections such as:

```markdown
# Today's notes

![[Daily Note.base]]

# Summary

# Good things from today

1.
2.
3.

# Things to improve from today

1.
2.
3.
```

Journal notes are created through the normal Unique Note workflow and adding the corresponding `Journal Template`, rather than depending on a rigid Daily Notes mechanism. This keeps the system flexible when writing about previous days.

---

## Project management

Project management lives inside `Actions/`.

Projects and Tasks are separate Entities because they have different operational characteristics, even though they share the same physical area of the vault.

Projects and Tasks templates both set a frontmatter and a body, to be used as reference for keeping a consistent format for all notes.

Projects contain bases that point to all Tasks and Meetings linked to the project itself.

In tasks, body checkboxes should describe the progressive completion of local steps, while the Task's properties describe the Task as a managed action.

The project-management layer is intentionally *simple*. MOSAIC defines the separation and relationships, but the exact statuses, reporting conventions, time tracking, and workflows should be developed to the needs of each user.

---


## Calendar

Calendar nodes live inside `Calendar/`. They will likely be linked many times especially to Actions and Journal nodes.

There are two types of nodes: Meetings and Events.

Meetings can be use to store appointments of any type. You may want to add the Work category for meetings related to work. Meetings can point to many Projects. This allows them to track all meetings for a particular project. Leave the Projects empty for meetings not related to any project, such as a personal meeting with a friend.

Events are a variant of Meetings to be used for everything which is not inherently a meeting, such as a concert, a trip or a medical appointment.

---


## Hotkeys

One single hotkey has been added:
- `Cmd+u` creates a new unique note in `Inbox/`.

Feel free to remove it and start from a blank set of custom hotkeys.

---


## License

Copyright © 2026 Riccardo Roberto De Lucia.

This Obsidian vault is distributed under the terms of the
[Apache License 2.0](LICENSE).

If you redistribute this vault, or a modified version containing
substantial portions of it, you must preserve the applicable copyright,
license, and attribution notices, including the notices contained in
the [NOTICE](NOTICE) file.

When reusing material from this vault, attribution to the original
project is appreciated:

> Based on [MOSAIC](https://github.com/riccardodelucia/obsidian-mosaic)
> by Riccardo Roberto De Lucia.