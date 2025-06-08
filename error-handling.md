# Error Handling

Good error handling makes scripts safer and easier to debug.

## Halting with an Error

```csharp
if (somethingWentWrong) {
    ScriptError("Something went wrong: explain why!");
    return;
}
```

## User Input & Validation

```csharp
string folder = PromptChooseDirectory();
if (folder == null) {
    ScriptError("No folder selected!");
    return;
}
```

## Logging/Debugging

For debugging, use `ScriptMessage` to display values or checkpoints.

```csharp
ScriptMessage("Step 1 done.");
```

## Exceptions

Most exceptions will be shown by UTMT, but you can use `try/catch` for fine-grained control:

```csharp
try {
    // risky code
} catch (Exception ex) {
    ScriptError("Failed: " + ex.Message);
}
```