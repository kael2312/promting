Please create a production-quality setup script for Kiro IDE global resources with the following requirements.

# Context

I have a repository that contains shared AI resources for AWS Kiro IDE.

Current structure:

```txt id="qv9b5r"
repo/
 ├── .agent/
 │    ├── skills/
 │    ├── steering/
 │    └── hooks/
 │
 ├── scripts/
 │
 └── package.json
```

Kiro global scope location:

Windows:

```txt id="b3hhzz"
C:\Users\<username>\.kiro
```

macOS/Linux:

```txt id="zsw5pf"
~/.kiro
```

I want any developer to be able to clone the repository and run:

```bash id="q3p73n"
npm run setup:kiro
```

and automatically sync all shared resources into the user's global `.kiro` directory.

# Technical Requirements

Implement the solution using Node.js ONLY.

Do NOT use:

* shell scripts
* bash scripts
* Python

Use Node.js built-in modules only:

* `fs`
* `path`
* `os`

Priority goals:

* cross-platform compatibility
* Windows/macOS/Linux support
* recursive copy
* auto-create missing directories
* overwrite existing files
* clean logging
* maintainable architecture
* enterprise-friendly structure

# Mapping Rules

Do NOT copy the entire `.agent` folder directly.

Instead map folders like this:

```txt id="x6cah8"
.agent/skills    -> ~/.kiro/skills
.agent/steering  -> ~/.kiro/steering
.agent/hooks     -> ~/.kiro/hooks
```

# What I want you to generate

Please generate:

1. `package.json` script setup
2. Full implementation for:

   * `scripts/sync-kiro.js`
3. Clear console logging
4. Proper error handling
5. Code comments explaining the logic
6. Clean and scalable code structure
7. Enterprise-grade readability

# Additional Requirements

If a source folder does not exist, skip it gracefully instead of throwing an error.

Example:

* if `.agent/hooks` does not exist, the script should continue normally

At the end, print a summary like:

```txt id="3f9l83"
✅ Synced skills
✅ Synced steering
⚠️ hooks folder not found
```

# Bonus Features

If possible, also support:

* automatic OS detection
* dry-run mode
* future extensibility for version metadata
* modular helper functions

The final code should feel production-ready and suitable for a real engineering organization.
