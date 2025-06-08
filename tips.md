# Tips & Gotchas

- **Always** use `EnsureDataLoaded();` at the start of your script.
- Use `.Content` to get string values from UMT string objects (e.g., `room.Name.Content`).
- For code decompilation, use the recommended decompiler classes.
- Placed objects in GM:S2+ are in instance layers, not `room.GameObjects`.
- **Back up your project** before running scripts that change data!
- Use `ScriptMessage` and `ScriptError` for user feedback and debugging.
- You can use all .NET base libraries (e.g., `System.IO`, `System.Linq`).
- For batch operations, consider using `Parallel.ForEach` with progress bars.
- Some changes (like new objects) might require a reload to appear in the UTMT UI.
- If you’re not sure about a type’s properties, explore with the script panel’s autocomplete.

See [Further Reading](links.md) for more resources.
