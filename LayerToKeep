var dialog = new Window("dialog", "輸入名稱，請留意大小寫與空白鍵");
dialog.add("statictext", undefined, "要保留的圖層名稱(以逗號,隔開)：");
var inputText = dialog.add("edittext", undefined, "");
inputText.characters = 40;

dialog.add("button", undefined, "確定", { name: "ok" });
if (dialog.show() == 1) {
  var layersToKeep = inputText.text.split(",");
  alert("以下是將會保留的圖層名稱：" + layersToKeep.join(", "));
}

var doc = app.activeDocument;
function processLayers(layers) {
  for (var i = layers.length - 1; i >= 0; i--) {
    var layer = layers[i];
    if (layer.typename == "LayerSet") {
      processLayers(layer.layers);
      for (var j = layer.layers.length - 1; j >= 0; j--) {
        layer.layers[j].move(doc, ElementPlacement.PLACEATBEGINNING);
      }
      layer.remove();
    }
  }
}
processLayers(doc.layers);
for (var i = 0; i < doc.layers.length; i++) {
  doc.layers[i].visible = true;
}
for (var i = doc.layers.length - 1; i >= 0; i--) {
  var layerName = doc.layers[i].name;
  var shouldKeep = false;
  for (var j = 0; j < layersToKeep.length; j++) {
    if (layerName == layersToKeep[j]) {
      shouldKeep = true;
      break;
    }
  }
  if (!shouldKeep) {
    doc.layers[i].remove();
  }
}
