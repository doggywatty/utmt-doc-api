# Advanced Scripts

## Creating New Objects

```csharp
EnsureDataLoaded();

var obj = new UndertaleGameObject();
obj.Name = Data.Strings.MakeString("obj_custom");
obj.Sprite = Data.Sprites.FirstOrDefault(s => s.Name.Content == "spr_player");
Data.GameObjects.Add(obj);
ScriptMessage("Added new object: obj_custom");
```

---

## Adding an Instance to a Room

```csharp
EnsureDataLoaded();

var room = Data.Rooms[0];
var playerObj = Data.GameObjects.First(o => o.Name.Content == "obj_player");

// Find or create an instance layer
var instLayer = room.Layers.FirstOrDefault(l => l.LayerType == UndertaleRoom.LayerType.Instances);
if (instLayer == null) {
    instLayer = new UndertaleRoom.Layer() {
        LayerType = UndertaleRoom.LayerType.Instances,
        LayerName = Data.Strings.MakeString("Instances"),
        InstancesData = new UndertaleRoom.Layer.LayerInstancesData()
    };
    room.Layers.Add(instLayer);
}
var inst = new UndertaleRoom.GameObject();
inst.ObjectDefinition = playerObj;
inst.X = 100;
inst.Y = 100;
inst.InstanceID = Data.GeneralInfo.LastObj++;
instLayer.InstancesData.Instances.Add(inst);
room.GameObjects.Add(inst); // For compatibility

ScriptMessage("Added player instance to room!");
```

---

## Decompiling Code from an Event

```csharp
EnsureDataLoaded();

var obj = Data.GameObjects.First(o => o.Name.Content == "obj_player");
var createEvent = obj.Events.FirstOrDefault(ev => ev.EventType == UndertaleEventType.Create);
if (createEvent != null && createEvent.Actions.Count > 0) {
    var code = createEvent.Actions[0].Code;
    string gml = new Underanalyzer.Decompiler.DecompileContext(
        new GlobalDecompileContext(Data),
        code,
        Data.ToolInfo.DecompilerSettings
    ).DecompileToString();
    ScriptMessage(gml);
}
```

---

## Exporting All Sprites as PNG

```csharp
EnsureDataLoaded();
string exportDir = Path.Combine(Path.GetDirectoryName(FilePath), "Export_Sprites");
Directory.CreateDirectory(exportDir);

foreach (var sprite in Data.Sprites) {
    for (int i = 0; i < sprite.Frames.Count; i++) {
        var frame = sprite.Frames[i];
        var bmp = frame.Texture?.GetBitmap();
        if (bmp != null) {
            bmp.Save(Path.Combine(exportDir, $"{sprite.Name.Content}_{i}.png"));
        }
    }
}
ScriptMessage("Sprites exported!");
```