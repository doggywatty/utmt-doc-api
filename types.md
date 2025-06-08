# Types

This page explains the most common UMT scripting types.

---

## Data

The global entrypoint for all loaded resources.

**Properties:**
- `Rooms` — `List<UndertaleRoom>`
- `Sprites` — `List<UndertaleSprite>`
- `GameObjects` — `List<UndertaleGameObject>`
- `Code` — `List<UndertaleCode>`
- `Sounds`, `Backgrounds`, `Fonts`, etc.
- `Strings` — Access to all game strings
- `ToolInfo` — Tool settings, decompiler config

---

## UndertaleRoom

Represents a room (level), with layers and placed objects.

**Key properties:**
- `Name.Content` — Room name (as string)
- `Layers` — List of layers (GM:S 2+)
- `GameObjects` — Placed objects (legacy/GM:S1)
- `Width`, `Height` — Room size (uint)
- `Views`, `Backgrounds`, `Tiles` — Other room data

**Accessing placed objects (GM:S 2+):**
```csharp
foreach (var layer in room.Layers) {
    if (layer.LayerType == UndertaleRoom.LayerType.Instances && layer.InstancesData?.Instances != null) {
        foreach (var inst in layer.InstancesData.Instances) {
            // Each inst is a GameObject instance!
        }
    }
}
```

---

## UndertaleGameObject

Represents an object type (not a placed instance).

- `Name.Content` — Name of the object
- `Sprite` — Main sprite reference
- `Events` — List of events (Create, Step, etc.)
- `Persistent` — Whether the object is persistent

---

## UndertaleCode

Represents any code resource (script, event, instance code).

- `Name.Content` — Name for scripts/standalone code
- To get readable GML, see [Examples](examples.md).

---

## Other Notable Types

- **UndertaleSprite:** `Name.Content`, `Frames`, `Width`, `Height`
- **UndertaleSound:** `Name.Content`, `AudioFile`
- **UndertaleFont:** `Name.Content`, `FontName`, `Size`

For more, explore code in [Advanced Scripts](advanced.md).