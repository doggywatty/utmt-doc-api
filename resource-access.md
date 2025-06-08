# Resource Access

The global `Data` object gives you access to **all loaded assets**.

## Main Asset Lists

- `Data.Rooms` — List of all rooms (levels)
- `Data.Sprites` — List of all sprites
- `Data.GameObjects` — List of all object types
- `Data.Code` — List of all code resources (scripts, events, etc.)
- `Data.Sounds`, `Data.Backgrounds`, `Data.Fonts`, etc.

## Iterating Over Resources

```csharp
foreach (var room in Data.Rooms) {
    ScriptMessage("Room: " + room.Name.Content);
}
```

```csharp
foreach (var code in Data.Code) {
    if (code.Name.Content.StartsWith("scr_")) {
        // do something with script code
    }
}
```

## Filtering and Searching

```csharp
// Find object by name
var obj = Data.GameObjects.FirstOrDefault(o => o.Name.Content == "obj_player");

// Find all rooms with "boss" in their name
var bossRooms = Data.Rooms.Where(r => r.Name.Content.ToLower().Contains("boss"));
```

## Asset Creation

You can create new assets with constructors, then add them to the relevant list:

```csharp
var newSprite = new UndertaleSprite();
newSprite.Name = Data.Strings.MakeString("spr_new");
Data.Sprites.Add(newSprite);
```

**Tip:** Some asset types (like code or objects) require more setup. See [Advanced Scripts](advanced.md).

See [Types](types.md) for a rundown of asset classes.