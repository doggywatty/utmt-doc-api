# Getting Started

## Writing Your First Script

1. **Open UMT** and load your game project.
2. **Go to the Scripts panel.**
3. **Create a new `.csx` script.**
4. **Start every script with:**  
   ```csharp
   EnsureDataLoaded();
   ```
   This ensures all resources are loaded before your script runs.

## Script Structure

- **Top-level C# code** (no `Main` method or class required).
- **Automatic references**: All UMT/UndertaleModLib types, plus .NET (`System`, `System.IO`, etc.)
- **Global objects**: `Data`, `FilePath`, and UI helpers (`ScriptMessage`, etc.).

## Example: Hello World

```csharp
EnsureDataLoaded();
ScriptMessage("Hello, world! UMT scripting works!");
```

## Best Practices

- Always use `EnsureDataLoaded();`.
- Use `ScriptMessage` to show results or debug info.
- Use `ScriptError` to halt with a clear error.
- Save often and back up your project!

For more, see [Resource Access](resource-access.md).