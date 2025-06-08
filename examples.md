# Example Scripts

## Export All Code Resources as GML

```csharp
EnsureDataLoaded();
string exportDir = Path.Combine(Path.GetDirectoryName(FilePath), "Export_Code");
Directory.CreateDirectory(exportDir);

foreach (var code in Data.Code) {
    string gml = new Underanalyzer.Decompiler.DecompileContext(
        new GlobalDecompileContext(Data),
        code,
        Data.ToolInfo.DecompilerSettings
    ).DecompileToString();
    File.WriteAllText(Path.Combine(exportDir, code.Name.Content + ".gml"), gml);
}
ScriptMessage("Code export complete!");
```

---

## Export All Room Instances as CSV

```csharp
EnsureDataLoaded();
string exportDir = Path.Combine(Path.GetDirectoryName(FilePath), "Export_Rooms");
Directory.CreateDirectory(exportDir);

foreach (var room in Data.Rooms) {
    var safeName = string.Concat(room.Name.Content.Split(Path.GetInvalidFileNameChars()));
    var csvPath = Path.Combine(exportDir, $"{safeName}.csv");
    var sb = new System.Text.StringBuilder();
    sb.AppendLine("Layer,ObjectName,InstanceID,X,Y,CreationCode");

    foreach (var layer in room.Layers)
        if (layer.LayerType == UndertaleRoom.LayerType.Instances && layer.InstancesData?.Instances != null)
            foreach (var inst in layer.InstancesData.Instances) {
                string codeText = "";
                if (inst.CreationCode != null)
                    codeText = new Underanalyzer.Decompiler.DecompileContext(
                        new GlobalDecompileContext(Data),
                        inst.CreationCode,
                        Data.ToolInfo.DecompilerSettings
                    ).DecompileToString().Replace("\n", "\\n").Replace("\"", "\"\"");
                sb.AppendLine($"{layer.LayerName.Content},{inst.ObjectDefinition?.Name?.Content},{inst.InstanceID},{inst.X},{inst.Y},\"{codeText}\"");
            }
    File.WriteAllText(csvPath, sb.ToString());
}
ScriptMessage("Room export complete!");
```

---

## Batch Edit: Move All Player Objects

```csharp
EnsureDataLoaded();
int moved = 0;
foreach (var room in Data.Rooms)
    foreach (var layer in room.Layers)
        if (layer.LayerType == UndertaleRoom.LayerType.Instances && layer.InstancesData?.Instances != null)
            foreach (var inst in layer.InstancesData.Instances)
                if (inst.ObjectDefinition?.Name?.Content == "obj_player") {
                    inst.X += 32;
                    moved++;
                }
ScriptMessage($"Moved {moved} player objects.");
```

See [Advanced Scripts](advanced.md) for more!