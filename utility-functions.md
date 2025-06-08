# Utility & UI Functions

UTMT scripting provides built-in helpers for interacting with the user and the tool itself.

## Dialogs

- `ScriptMessage("text")`  
  Show a message dialog.

- `ScriptError("error text")`  
  Show an error dialog and halt the script.

## File & Directory Pickers

- `PromptChooseDirectory()` — Opens a dialog to choose a folder. Returns the path or `null`.
- `PromptChooseFile()` — Opens a dialog to choose a file. Returns the path or `null`.

## Progress Bars

For long-running scripts:

```csharp
SetProgressBar(null, "Exporting...", 0, Data.Rooms.Count);
StartProgressBarUpdater();

await Task.Run(() => Parallel.ForEach(Data.Rooms, room => {
    // ... your code ...
    IncrementProgressParallel();
}));

await StopProgressBarUpdater();
HideProgressBar();
```

## Other Utilities

- `FilePath` — Path to the loaded project file (e.g., `.win`, `.undertale`)
- `Directory.CreateDirectory(path)` — Standard C# for making folders

See [Examples](examples.md) for practical use.
