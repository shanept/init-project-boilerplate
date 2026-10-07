# init-project-boilerplate

This skill creates the initial project documents and gives your coding agent consistent guidance for turning your ideas into specifications and, later, an implementation. You can use it with any language or framework. You do not need to choose a technology stack before getting started.

## Getting started

Ask your coding agent to install the skill:

```text
Install the skill shanept/init-project-boilerplate
```

Open an empty project directory in your agent and run:

```text
/init-project-boilerplate
```

Tell the agent what you want to build, who will use it, and any constraints you already know. Also tell it where you want to track bugs and implementation work. You can choose no tracker or leave that decision for later.

For example:

> I want to build an application for a community tool library. Volunteers need to record loans and see which tools are available. It will initially serve one location. We haven't chosen an issue tracker yet; leave that decision open.

The agent will ask for any missing information. If the directory already contains files, it will clarify what you want to add, update, or preserve before making changes.

## What you get

```text
<project-root>/
├── spec/
│   ├── CONTEXT.md
│   ├── SPECIFICATION-AUTHORING-RULES.md
│   └── authoring-rules/
├── src/
├── .gitignore
├── AGENTS.md
└── README.md
```

Your application's **README.md** introduces the project to its users and contributors. It starts with the information you provide and grows as the application takes shape.

**AGENTS.md** guides your coding agent: where to find the specifications, how to handle unanswered questions, where issues are tracked, and how to organize commits. **spec/CONTEXT.md** gives shared domain terms a consistent meaning.

The **spec/** directory also contains the specification authoring rules. These cover document structure, decisions, data definitions, contracts, and changes. You can adapt them as your application's needs evolve.

**src/** starts empty, ready for application code. **.gitignore** contains ignore rules suited to what is known about the project.

## What comes next

After initialization, work with your agent to develop the application's requirements and resolve the decisions needed for your first piece of implementation. The foundation does not include application code, installed dependencies, framework scaffolding, or an initialized Git repository.

As development progresses, the agent maintains your application's README so readers can understand its current capabilities and find verified setup and usage instructions. Planned features remain distinguishable from working functionality.

You can run the skill again to add missing documents or refresh selected files. Existing project customizations are preserved unless you ask to change them.
