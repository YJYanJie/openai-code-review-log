file
diff --git a/docs/front/mock/mock02.json b/docs/front/mock/mock02.json
new file mode 100644
index 0e4045f..e5b6f3e
--- a/docs/front/js/goSamples.js
+++ b/docs/front/js/goSamples.js
@@ -279,6 +279,7 @@
   "dataFlowVertical.html",
   "dynamicPorts.html",
   "planogram.html",
+  "regrouping.html",
   "seatingChart.html",
   "swimBands.html",
   "swimLanes.html",
diff --git a/docs/front/samples/regrouping.html b/docs/front/samples/regrouping.html
new file mode 100644
index 0000000..d7b9c0a
--- /dev/null
+++ b/docs/front/samples/regrouping.html
@@ -0,0 +1,79 @@
+<!DOCTYPE html>
+<html lang="en">
+<head>
+    <meta charset="UTF-8">
+    <meta name="viewport" content="width=device-width, initial-scale=1.0">
+    <title>Regrouping</title>
+    <script src="../go.js"></script>
+    <script src="regrouping.js"></script>
+    <style>
+        html, body {
+            height: 100%;
+            width: 100%;
+            padding: 0;
+            margin: 0;
+            overflow: hidden;
+        }
+
+        .myButton {
+            width: 100px;
+            height: 30px;
+            background: #ddd;
+            border: none;
+            border-radius: 4px;
+            margin: 10px;
+        }
+
+        .myButton:hover {
+            background: #ccc;
+        }
+
+        #myDiagram .go.Node {
+            selection-box: visible;
+        }
+
+        #myDiagram .go.Node {
+            background: #EFEFEF;
+            border-width: 1px;
+            border-color: #9D9D9D;
+        }
+
+        #myDiagram .go.Node-selected {
+            background: #C6E4FF;
+            border: 2px solid #4D90FE;
+        }
+
+        #myDiagram .go.Link {
+            // background: #C6E4FF;
+            // stroke: #4D90FE;
+            // stroke-width: 2px;
+            // visibility: hidden;
+        }
+
+        #myDiagram .go.Node .ValidatingLabel {
+            color: #B30000;
+            font-weight: bold;
+        }
+
+        .ValidatingLabel {
+            color: #B30000;
+            font-weight: bold;
+        }
+    </style>
+</head>
+<body>
+    <div id="sample"></div>
+
+    <div id="myButtonPanel">
+        <div class="myButton" onclick="addNode()">Add Node</div>
+        <div class="myButton" onclick="removeNode()">Remove Node</div>
+        <div class="myButton" onclick="addGroup()">Add Group</div>
+        <div class="myButton" onclick="removeGroup()">Remove Group</div>
+    </div>
+
+    <div id="myDiagramDiv" style="width:100%;height:100%;border:1px solid #000;"></div>
+
+    <script>
+        function init() {
+            myDiagram = go.Diagram("myDiagramDiv");
+            myDiagram.layout = new go.LayeredDigraphLayout();
+            myDiagram.model = new go.GraphLinksModel({
+                nodeDataArray: [
+                    { key: "A" },
+                    { key: "B" },
+                    { key: "C" },
+                    { key: "D" },
+                    { key: "E" }
+                ],
+                linkDataArray: [
+                    { from: "A", to: "B" },
+                    { from: "A", to: "C" },
+                    { from: "A", to: "D" },
+                    { from: "B", to: "E" },
+                    { from: "C", to: "E" },
+                    { from: "D", to: "E" }
+                ]
+            });
+            // Arrange the nodes and links.
+            myDiagram.layout.doLayout();
+        }
+
+        function addNode() {
+            var model = myDiagram.model;
+            var key = model.makeUniqueKey();
+            var nodeData = { key: key, text: "