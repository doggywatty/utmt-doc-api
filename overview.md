# Overview

UndertaleModTool (UMT) includes a robust, C#-based scripting system for automating resource export/import, batch-editing, and extending the tool’s functionality.

**Key Features:**
- Full access to all loaded game data, including rooms, objects, sprites, sounds, code, and more.
- Scripts run in the context of an open project (`.win`, `.deltarune`, `.undertale`, etc.).
- Use all standard .NET and C# 9 features.
- Powerful UI integration: show dialogs, get user input, display progress bars.
- Direct resource editing, batch operations, and export/import workflows.

## When to Use Scripting

- Exporting large amounts of data (code, sprites, sounds, etc.)
- Batch-modifying or analyzing assets
- One-off fixes or custom import/export tools
- Automating repetitive editing tasks

**Note:** Scripts can change your project irreversibly. Always make backups before running scripts!

See [Getting Started](getting-started.md) for your first script.