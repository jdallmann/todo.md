# todo.md format

A complete primer on the whys and hows of `todo.md`, a Markdown-friendly adaptation of the classic [todo.txt](https://github.com/todotxt/todo.txt) format.

The first and most important rule of `todo.md`:

> A single task line in your `todo.md` file represents a single task, organized cleanly under Markdown project headers.

## Why plain text and Markdown?

Plain text is software and operating system agnostic. It's searchable, portable, lightweight, and easily manipulated. By adapting the `todo.txt` format to standard Markdown (`todo.md`), your task list remains completely portable in plain text while gaining native support for interactive checkboxes and collapsible section headers in any standard Markdown viewer or editor (like GitHub, Obsidian, Notion, or VS Code). 

It works when someone else's web server is down or your database file is corrupt. There's no exporting and importing, no proprietary databases, and no company-induced rules on what you can and can't do with it.

## The 3 axes of an effective todo list

Using special notation and Markdown structure in `todo.md`, you can create a list that's sliceable by 3 key axes:

### Priority

Your todo list should be able to tell you what's the next most important thing for you to get done—either by project or by context or overall. You can optionally assign tasks a priority that'll bubble them up to the top of a project list when sorted alphabetically.

### Project

The only way to move a big project forward is to tackle a small subtask associated with it. Your `todo.md` groups all the tasks specific to a project under a level-2 Markdown header (`## Project`).

In order to move along a project like "Cleaning out the garage," my task list should give me the next logical action to take in order to move that project along. "Clean out the garage" isn't a good todo item; but "Call Goodwill to schedule pickup" under the `## GarageSale` (or `## Clean out garage`) header is.

### Context

*Getting Things Done* author David Allen suggests splitting up your task lists by context—i.e., the place and situation where you'll work on the job. Messages that you need to send go in the `@email` context; calls to be made `@phone`, household projects `@home`.

That way, when you've got a few minutes in the car with your cell phone, you can easily search your `@phone` tasks and make a call or two while you have the opportunity.

This is all possible inside `todo.md`.

---

## `todo.md` format rules

![todo.md format illustration](todo_md_description.jfif)

Your `todo.md` is a plain text Markdown file. To take advantage of structured task metadata like priority, projects, context, creation, and completion date, there are a few simple but flexible file format rules.

Philosophically, the `todo.md` file format has three goals:

1. The file contents should be human-readable without requiring any tools other than a plain text viewer or editor.
2. The file should render natively as a clean, interactive task list with grouped sections in any standard Markdown viewer.
3. A user can manipulate the file contents in a plain text editor in sensible, expected ways. For example, a text editor that can sort lines alphabetically within a project section should be able to sort your task list in a meaningful way.

These goals are why tasks begin with standard Markdown checkboxes (`- [ ] ` and `- [x] `), followed immediately by priority and/or dates. When sorting lines within a project section, incomplete tasks (`- [ ]`) naturally sort above completed tasks (`- [x]`), and prioritized tasks sort by importance and time.

Here are the rest.

### Projects: Structural Rule

Unlike `todo.txt` which uses inline `+Project` tags, `todo.md` groups tasks together under Markdown level-2 headers (`## Project`). 

- **Projects are defined by `## ProjectName` headers.** All task lines following a `## Project` header belong to that project until the next `##` header appears.
- Tasks that do not belong to a specific project can be placed at the top of the file before the first `##` header, or under a general header such as `## General` or `## Inbox`.
- **Optional sub-projects or inline tags:** If a task belongs to multiple projects, it should live under its primary `## Project` header, or optionally reference secondary projects inline if your workflow requires it.

### Incomplete Tasks: 4 Format Rules

The beauty of `todo.md` is that it's flexible; the fields you can attach to each task are only limited by your imagination. To get started, group tasks under `## Project` headers, start each task with `- [ ] `, and use special notation to indicate task context (e.g., `@phone`) and priority (e.g., `(A)`).

A `todo.md` file might look like the following:

```markdown
- [ ] (A) Thank Mom for the meatballs @phone
- [ ] @GroceryStore pies

## GarageSale
- [ ] (B) Schedule Goodwill pickup @phone
- [ ] Post signs around the neighborhood
```

A search and filter for the `@phone` contextual items would output:

```markdown
- [ ] (A) Thank Mom for the meatballs @phone
- [ ] (B) Schedule Goodwill pickup @phone
```

To just see the `GarageSale` project items, you simply look under the `## GarageSale` header in your file or Markdown viewer:

```markdown
## GarageSale
- [ ] (B) Schedule Goodwill pickup @phone
- [ ] Post signs around the neighborhood
```

There are four formatting rules for current todos:

#### Rule 1: Every incomplete task starts with `- [ ] `

Every incomplete task must begin on a new line with a hyphen, a space, an open bracket, a single space, a close bracket, and a space (`- [ ] `). This allows standard Markdown viewers to render an unchecked checkbox.

#### Rule 2: If priority exists, it ALWAYS appears first after the checkbox.

The priority is an uppercase character from A–Z enclosed in parentheses and followed by a space, placed directly after `- [ ] `.

This task has a priority:

```markdown
- [ ] (A) Call Mom
```

These tasks do **not** have any priorities:

```markdown
- [ ] Really gotta call Mom (A) @phone @someday
- [ ] (b) Get back to the boss
- [ ] (B)->Submit TPS report
```

#### Rule 3: A task's creation date may optionally appear directly after priority and a space.

If there is no priority, the creation date appears directly after the `- [ ] ` checkbox and a space. If the creation date exists, it should be in the format `YYYY-MM-DD`.

These tasks have creation dates:

```markdown
## TodoMd
- [ ] 2011-03-02 Document task format
- [ ] (A) 2011-03-02 Call Mom
```

This task doesn't have a creation date:

```markdown
- [ ] (A) Call Mom 2011-03-02
```

#### Rule 4: Contexts may appear anywhere in the line after priority/prepended date.

A context is preceded by a single space and an at-sign (`@`). A context contains any non-whitespace character. A task may have zero, one, or more than one contexts included in it.

For example, this task is under the `## Family` project and is part of the `@iphone` and `@phone` contexts:

```markdown
## Family
- [ ] (A) Call Mom @iphone @phone
```

This task has no contexts in it:

```markdown
- [ ] Email SoAndSo at soandso@example.com
```

---

### Complete Tasks: 2 Format Rules

Two things indicate that a task has been completed.

#### Rule 1: A completed task starts with `- [x] `

If a task starts with `- [x] ` (a hyphen, space, open bracket, lowercase `x`, close bracket, and space), it is marked as complete. *(Note: `- [x]` without a leading space inside the brackets may also be tolerated by some parsers, though `- [x] ` is standard Markdown).*

This is a complete task:

```markdown
- [x] 2011-03-03 Call Mom
```

These are **not** complete tasks:

```markdown
- [ ] xylophone lesson
x 2012-01-01 Make resolutions
- [ ] (A) x Find ticket prices
```

We use `- [x] ` so that Markdown viewers render a checked box, and because `[x]` sorts below `[ ]` in ASCII alphabetical order, meaning completed tasks sort to the bottom of a project's task list using standard sort tools.

#### Rule 2: The date of completion appears directly after the `- [x] `, separated by a space.

For example:

```markdown
## TodoTxtTouch
- [x] 2011-03-02 2011-03-01 Review Tim's pull request @github
```

If you've prepended the creation date to your task, on completion it will appear directly after the completion date. This is so your completed tasks sort chronologically by completion date using standard sort tools. Many clients discard priority on task completion so that completed tasks sort cleanly together. To preserve it, use the `key:value` format described below (e.g., `pri:A`).

With the completed date (optional or required depending on your parser), if you've used the prepended creation date, you can calculate how many days it took to complete a task.

---

### Additional File Format Definitions

Tool developers may define additional formatting rules for extra metadata.

Developers should use the format `key:value` to define additional metadata (e.g., `due:2010-01-02` as a due date).

Both `key` and `value` must consist of non-whitespace characters, which are not colons. Only one colon separates the `key` and `value`.
