<template>
  <div></div>
</template>

<script>

import * as go from "gojs";

export default {
  name: "diagram",
  props: ["modelData"],
  mounted: function() {

    const $ = go.GraphObject.make;

    var self = this;
    var myDiagram =
      $(go.Diagram, this.$el,
        {
          //layout: $(go.TreeLayout, { angle: 90, arrangement: go.TreeLayout.ArrangementHorizontal }),
          //layout: $(go.ForceDirectedLayout, { }),
          "undoManager.isEnabled": true,
          // Model ChangedEvents get passed up to component users
          //"ModelChanged": function(e) { self.$emit("model-changed", e); },
          //"ChangedSelection": function(e) { self.$emit("changed-selection", e); }
        });

    /*
    myDiagram.nodeTemplate =
      $(go.Node, "Auto",
        $(go.Shape,
          {
            fill: "white", strokeWidth: 0,
            portId: "", fromLinkable: true, toLinkable: true, cursor: "pointer"
          },
          new go.Binding("fill", "color")),
        $(go.TextBlock,
          { margin: 8, editable: true },
          new go.Binding("text").makeTwoWay())
      );

    myDiagram.linkTemplate =
      $(go.Link,
        { relinkableFrom: true, relinkableTo: true },
        $(go.Shape),
        $(go.Shape, { toArrow: "OpenTriangle" })
      );
    */

    var portSize = new go.Size(8, 8);

    // the node template
    // includes a panel on each side with an itemArray of panels containing ports
    myDiagram.nodeTemplate =
      $(go.Node, "Table",
        {
          locationObjectName: "BODY",
          locationSpot: go.Spot.Center,
          selectionObjectName: "BODY",
        },
        new go.Binding("location", "loc", go.Point.parse).makeTwoWay(go.Point.stringify),

        // the body
        $(go.Panel, "Auto",
          {
            row: 1, column: 1, name: "BODY",
            stretch: go.GraphObject.Fill
          },
          $(go.Shape, "Rectangle",
            {
              fill: "#dbf6cb", 
              stroke: null, 
              strokeWidth: 0,
              //minSize: new go.Size(80, 80)
            },
            new go.Binding("minSize", "size", go.Size.parse).makeTwoWay(go.Size.stringify),
          ),
          $(go.TextBlock,
            { margin: 10, textAlign: "center", font: "bold 14px Segoe UI,sans-serif", stroke: "#484848", editable: true },
            new go.Binding("text", "name").makeTwoWay())
        ),  // end Auto Panel body

        // the Panel holding the left port elements, which are themselves Panels,
        // created for each item in the itemArray, bound to data.leftArray
        $(go.Panel, "Vertical",
          new go.Binding("itemArray", "leftArray"),
          {
            row: 1, column: 0,
            itemTemplate:
              $(go.Panel,
                {
                  _side: "left",  // internal property to make it easier to tell which side it's on
                  fromSpot: go.Spot.Left, toSpot: go.Spot.Left,
                  fromLinkable: true, toLinkable: true, cursor: "pointer",
                },
                new go.Binding("portId", "portId"),
                $(go.Shape, "Rectangle",
                  {
                    stroke: null, strokeWidth: 0,
                    desiredSize: portSize,
                    margin: new go.Margin(1, 0)
                  },
                  new go.Binding("fill", "portColor"))
              )  // end itemTemplate
          }
        ),  // end Vertical Panel

        // the Panel holding the top port elements, which are themselves Panels,
        // created for each item in the itemArray, bound to data.topArray
        $(go.Panel, "Horizontal",
          new go.Binding("itemArray", "topArray"),
          {
            row: 0, column: 1,
            itemTemplate:
              $(go.Panel,
                {
                  _side: "top",
                  fromSpot: go.Spot.Top, toSpot: go.Spot.Top,
                  fromLinkable: true, toLinkable: true, cursor: "pointer",
                },
                new go.Binding("portId", "portId"),
                $(go.Shape, "Rectangle",
                  {
                    stroke: null, strokeWidth: 0,
                    desiredSize: portSize,
                    margin: new go.Margin(0, 1)
                  },
                  new go.Binding("fill", "portColor"))
              )  // end itemTemplate
          }
        ),  // end Horizontal Panel

        // the Panel holding the right port elements, which are themselves Panels,
        // created for each item in the itemArray, bound to data.rightArray
        $(go.Panel, "Vertical",
          new go.Binding("itemArray", "rightArray"),
          {
            row: 1, column: 2,
            itemTemplate:
              $(go.Panel,
                {
                  _side: "right",
                  fromSpot: go.Spot.Right, toSpot: go.Spot.Right,
                  fromLinkable: true, toLinkable: true, cursor: "pointer",
                },
                new go.Binding("portId", "portId"),
                $(go.Shape, "Rectangle",
                  {
                    stroke: null, strokeWidth: 0,
                    desiredSize: portSize,
                    margin: new go.Margin(1, 0)
                  },
                  new go.Binding("fill", "portColor"))
              )  // end itemTemplate
          }
        ),  // end Vertical Panel

        // the Panel holding the bottom port elements, which are themselves Panels,
        // created for each item in the itemArray, bound to data.bottomArray
        $(go.Panel, "Horizontal",
          new go.Binding("itemArray", "bottomArray"),
          {
            row: 2, column: 1,
            itemTemplate:
              $(go.Panel,
                {
                  _side: "bottom",
                  fromSpot: go.Spot.Bottom, toSpot: go.Spot.Bottom,
                  fromLinkable: true, toLinkable: true, cursor: "pointer",
                },
                new go.Binding("portId", "portId"),
                $(go.Shape, "Rectangle",
                  {
                    stroke: null, strokeWidth: 0,
                    desiredSize: portSize,
                    margin: new go.Margin(0, 1)
                  },
                  new go.Binding("fill", "portColor"))
              )  // end itemTemplate
          }
        )  // end Horizontal Panel
      );  // end Node

    // This custom-routing Link class tries to separate parallel links from each other.
    // This assumes that ports are lined up in a row/column on a side of the node.
    function CustomLink() {
      go.Link.call(this);
    };
    go.Diagram.inherit(CustomLink, go.Link);

    CustomLink.prototype.findSidePortIndexAndCount = function(node, port) {
      var nodedata = node.data;
      if (nodedata !== null) {
        var portdata = port.data;
        var side = port._side;
        var arr = nodedata[side + "Array"];
        var len = arr.length;
        for (var i = 0; i < len; i++) {
          if (arr[i] === portdata) return [i, len];
        }
      }
      return [-1, len];
    };

    CustomLink.prototype.computeEndSegmentLength = function(node, port, spot, from) {
      var esl = go.Link.prototype.computeEndSegmentLength.call(this, node, port, spot, from);
      var other = this.getOtherPort(port);
      if (port !== null && other !== null) {
        var thispt = port.getDocumentPoint(this.computeSpot(from));
        var otherpt = other.getDocumentPoint(this.computeSpot(!from));
        if (Math.abs(thispt.x - otherpt.x) > 20 || Math.abs(thispt.y - otherpt.y) > 20) {
          var info = this.findSidePortIndexAndCount(node, port);
          var idx = info[0];
          var count = info[1];
          if (port._side == "top" || port._side == "bottom") {
            if (otherpt.x < thispt.x) {
              return esl + 4 + idx * 8;
            } else {
              return esl + (count - idx - 1) * 8;
            }
          } else {  // left or right
            if (otherpt.y < thispt.y) {
              return esl + 4 + idx * 8;
            } else {
              return esl + (count - idx - 1) * 8;
            }
          }
        }
      }
      return esl;
    };

    CustomLink.prototype.hasCurviness = function() {
      if (isNaN(this.curviness)) return true;
      return go.Link.prototype.hasCurviness.call(this);
    };

    CustomLink.prototype.computeCurviness = function() {
      if (isNaN(this.curviness)) {
        var fromnode = this.fromNode;
        var fromport = this.fromPort;
        var fromspot = this.computeSpot(true);
        var frompt = fromport.getDocumentPoint(fromspot);
        var tonode = this.toNode;
        var toport = this.toPort;
        var tospot = this.computeSpot(false);
        var topt = toport.getDocumentPoint(tospot);
        if (Math.abs(frompt.x - topt.x) > 20 || Math.abs(frompt.y - topt.y) > 20) {
          if ((fromspot.equals(go.Spot.Left) || fromspot.equals(go.Spot.Right)) &&
            (tospot.equals(go.Spot.Left) || tospot.equals(go.Spot.Right))) {
            var fromseglen = this.computeEndSegmentLength(fromnode, fromport, fromspot, true);
            var toseglen = this.computeEndSegmentLength(tonode, toport, tospot, false);
            var c = (fromseglen - toseglen) / 2;
            if (frompt.x + fromseglen >= topt.x - toseglen) {
              if (frompt.y < topt.y) return c;
              if (frompt.y > topt.y) return -c;
            }
          } else if ((fromspot.equals(go.Spot.Top) || fromspot.equals(go.Spot.Bottom)) &&
            (tospot.equals(go.Spot.Top) || tospot.equals(go.Spot.Bottom))) {
            var fromseglen = this.computeEndSegmentLength(fromnode, fromport, fromspot, true);
            var toseglen = this.computeEndSegmentLength(tonode, toport, tospot, false);
            var c = (fromseglen - toseglen) / 2;
            if (frompt.x + fromseglen >= topt.x - toseglen) {
              if (frompt.y < topt.y) return c;
              if (frompt.y > topt.y) return -c;
            }
          }
        }
      }
      return go.Link.prototype.computeCurviness.call(this);
    };
    // end CustomLink class

    // an orthogonal link template, reshapable and relinkable
    myDiagram.linkTemplate =
      $(CustomLink,  // defined below
        {
          routing: go.Link.AvoidsNodes,
          corner: 4,
          curve: go.Link.JumpGap,
          reshapable: true,
          resegmentable: true,
          relinkableFrom: true,
          relinkableTo: true
        },
        new go.Binding("points").makeTwoWay(),
        $(go.Shape, { stroke: "#2F4F4F", strokeWidth: 2 })
      );


    this.diagram = myDiagram;
    this.updateModel(this.modelData);
  },
  watch: {
    modelData: function(val) { this.updateModel(val); }
  },
  methods: {
    model: function() { return this.diagram.model; },
    updateModel: function(val) {
      // No GoJS transaction permitted when replacing Diagram.model.
      if (val instanceof go.Model) {
        this.diagram.model = val;
      } else {
        var m = new go.GraphLinksModel()
        if (val) {
          for (var p in val) {
            m[p] = val[p];
          }
        }
        this.diagram.model = m;
      }
    },
    updateDiagramFromData: function() {
      this.diagram.startTransaction();
      // This is very general but very inefficient.
      // It would be better to modify the diagramData data by calling
      // Model.setDataProperty or Model.addNodeData, et al.
      this.diagram.updateAllRelationshipsFromData();
      this.diagram.updateAllTargetBindings();
      this.diagram.commitTransaction("updated");
    }
  },
  setup() {
    
  },
}
</script>
