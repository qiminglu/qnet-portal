<template>
  <div>
    <base-header class="pb-6">
      <div class="row align-items-center py-4">
        <div class="col-lg-6 col-7">
          <h6 class="h2 text-white d-inline-block mb-0">{{ $route.name }}</h6>
          <nav aria-label="breadcrumb" class="d-none d-md-inline-block ml-md-4">
            <route-breadcrumb />
          </nav>
        </div>
        <div class="col-lg-6 col-5 text-right">
          <base-button size="sm" type="neutral">New</base-button>
          <base-button size="sm" type="neutral">Filters</base-button>
        </div>
      </div>
    </base-header>

    <div class="container-fluid mt--6">
      <div class="row">

        <div class="col-lg-12">
          <card header-classes="bg-transparent">
            <!--
            <template v-slot:header>
              <h3 class="mb-0">System Topology</h3>
            </template>
            -->

            <div id="map" class="map-canvas" style="height: 300px; margin-bottom:20px"></div>

            <diagram ref="diag"
              v-bind:model-data="diagramData"
              style="border:solid 1px black; width:100%; height:600px">
            </diagram>

          </card>
        </div>

      </div>
    </div>
  </div>
</template>
<script>
import RouteBreadcrumb from "@/components/Breadcrumb/RouteBreadcrumb";
import BaseHeader from "@/components/BaseHeader";

import Diagram from "@/components/Diagram";

import { Loader } from "@googlemaps/js-api-loader";
const loader = new Loader({ apiKey: "" });

export default {
  components: {
    BaseHeader,
    RouteBreadcrumb,
    Diagram,
  },
  data() {
    return {
      diagramData: {  // passed to <diagram> as its modelData
      /*
        nodeDataArray: [
          { key: 1, text: "Optical Switch 1", color: "lightblue" },
          { key: 5, text: "Optical Switch 2", color: "lightblue" },
          { key: 2, text: "Q-Node 1", color: "orange" },
          { key: 3, text: "Q-Node 2", color: "orange" },
          { key: 4, text: "EPS", color: "pink" }
        ],
        linkDataArray: [
          { from: 1, to: 5 },
          { from: 5, to: 1 },
          { from: 2, to: 1 },
          { from: 4, to: 1 },
          { from: 3, to: 5 }
        ]
      */

        "class": "go.GraphLinksModel", 
        "copiesArrays": true, 
        "copiesArrayObjects": true, 
        "linkFromPortIdProperty": "fromPort", 
        "linkToPortIdProperty": "toPort", 
        "nodeDataArray": [ {
          "key":1, 
          "name":"Q-Node 1", 
          "loc":"100 100", 
          "size":"80 80", 
          "leftArray":[ 
            {"portColor":"#fae3d7", "portId":"left0"} 
          ], 
          "topArray":[ 
            {"portColor":"#d6effc", "portId":"top0"} 
          ], 
          "bottomArray":[ 
            {"portColor":"#ebe3fc", "portId":"bottom0"} 
          ], 
          "rightArray":[ 
            {"portColor":"#eaeef8", "portId":"c1tx"},
            {"portColor":"#fadfe5", "portId":"c1rx"},
            {"portColor":"#eaeef8", "portId":"c2tx"},
            {"portColor":"#fadfe5", "portId":"c2rx"},
          ] 
        }, {
          "key":2, 
          "name":"Optical Switch 1", 
          "loc":"320 150", 
          "size":"80 180", 
          "leftArray":[ 
            {"portColor":"#6cafdb", "portId":"lp0"},
            {"portColor":"#6cafdb", "portId":"lp1"},
            {"portColor":"#66d6d1", "portId":"lp2"},
            {"portColor":"#fae3d7", "portId":"lp3"},
            {"portColor":"#fae3d7", "portId":"lp4"},
            {"portColor":"#fae3d7", "portId":"lp5"},
            {"portColor":"#fae3d7", "portId":"lp6"},
            {"portColor":"#fae3d7", "portId":"lp7"},
            {"portColor":"#fae3d7", "portId":"lp8"},
          ], 
          "topArray":[ 
            {"portColor":"#d6effc", "portId":"top0"} 
          ], 
          "bottomArray":[ 
            {"portColor":"#eaeef8", "portId":"bottom0"},
            {"portColor":"#eaeef8", "portId":"bottom1"},
            {"portColor":"#6cafdb", "portId":"bottom2"} 
          ], 
          "rightArray":[  
            {"portColor":"#6cafdb", "portId":"rp1"},
            {"portColor":"#6cafdb", "portId":"rp2"},
            {"portColor":"#66d6d1", "portId":"rp3"},
            {"portColor":"#fae3d7", "portId":"rp4"},
          ] 
        }, {
          "key":3, 
          "name":"Optical Switch 2", 
          "loc":"500 200", 
          "size":"80 180", 
          "leftArray":[ 
            {"portColor":"#6cafdb", "portId":"lp1"},
            {"portColor":"#6cafdb", "portId":"lp2"},
            {"portColor":"#66d6d1", "portId":"lp3"},
            {"portColor":"#fae3d7", "portId":"lp4"},
          ], 
          "topArray":[ 
            {"portColor":"#66d6d1", "portId":"top0"} 
          ], 
          "bottomArray":[ 
            {"portColor":"#6cafdb", "portId":"bottom0"} 
          ], 
          "rightArray":[  
            {"portColor":"#6cafdb", "portId":"rp1"},
            {"portColor":"#6cafdb", "portId":"rp2"},
            {"portColor":"#66d6d1", "portId":"rp3"},
            {"portColor":"#fae3d7", "portId":"rp4"},
          ] 
        }, {
          "key":4, 
          "name":"EPS", 
          "loc":"100 300", 
          "size":"80 60", 
          "leftArray":[ 
            {"portColor":"#fae3d7", "portId":"left0"} 
          ], 
          "topArray":[ 
            {"portColor":"#6cafdb", "portId":"top0"} 
          ], 
          "bottomArray":[ 
            {"portColor":"#6cafdb", "portId":"bottom0"} 
          ], 
          "rightArray":[ 
            {"portColor":"#6cafdb", "portId":"c1tx"},
            {"portColor":"#66d6d1", "portId":"c2tx"} 
          ]
        }, {
          "key":5, 
          "name":"Q-Node 2", 
          "loc":"700 100", 
          "size":"80 80", 
          "leftArray":[ 
            {"portColor":"#eaeef8", "portId":"c1tx"},
            {"portColor":"#fadfe5", "portId":"c1rx"},
            {"portColor":"#eaeef8", "portId":"c2tx"},
            {"portColor":"#fadfe5", "portId":"c2rx"},
          ], 
          "topArray":[ 
            {"portColor":"#d6effc", "portId":"top0"} 
          ], 
          "bottomArray":[ 
            {"portColor":"#ebe3fc", "portId":"bottom0"} 
          ], 
          "rightArray":[ 
            {"portColor":"#fae3d7", "portId":"left0"} 
          ] 
        } ], 
        "linkDataArray": [ 
          {"from":4, "to":2, "fromPort":"c1tx", "toPort":"lp7"}, 
          {"from":4, "to":2, "fromPort":"c2tx", "toPort":"lp8"}, 
          {"from":2, "to":3, "fromPort":"rp1", "toPort":"lp1"}, 
          {"from":2, "to":3, "fromPort":"rp2", "toPort":"lp2"}, 
          {"from":2, "to":3, "fromPort":"rp3", "toPort":"lp3"}, 
          {"from":2, "to":3, "fromPort":"rp4", "toPort":"lp4"}, 
          {"from":1, "to":2, "fromPort":"c1tx", "toPort":"lp1"}, 
          {"from":1, "to":2, "fromPort":"c1rx", "toPort":"lp2"}, 
          {"from":1, "to":2, "fromPort":"c2tx", "toPort":"lp3"}, 
          {"from":1, "to":2, "fromPort":"c2rx", "toPort":"lp4"}, 
          {"from":5, "to":3, "fromPort":"c1tx", "toPort":"rp1"}, 
          {"from":5, "to":3, "fromPort":"c1rx", "toPort":"rp2"}, 
          {"from":5, "to":3, "fromPort":"c2tx", "toPort":"rp3"}, 
          {"from":5, "to":3, "fromPort":"c2rx", "toPort":"rp4"}, 
        ]
        /*
        "nodeDataArray": [ {
          "key":1, 
          "name":"Q-Node 1", 
          "loc":"100 100", 
          "size":"80 80", 
          "leftArray":[ 
            {"portColor":"#fae3d7", "portId":"left0"} 
          ], 
          "topArray":[ 
            {"portColor":"#d6effc", "portId":"top0"} 
          ], 
          "bottomArray":[ 
            {"portColor":"#ebe3fc", "portId":"bottom0"} 
          ], 
          "rightArray":[ 
            {"portColor":"#eaeef8", "portId":"c1tx"},
            {"portColor":"#fadfe5", "portId":"c1rx"},
            {"portColor":"#eaeef8", "portId":"c2tx"},
            {"portColor":"#fadfe5", "portId":"c2rx"},
          ] 
        }, {
          "key":2, 
          "name":"Optical Switch 1", 
          "loc":"320 150", 
          "size":"80 180", 
          "leftArray":[ 
            {"portColor":"#6cafdb", "portId":"lp0"},
            {"portColor":"#6cafdb", "portId":"lp1"},
            {"portColor":"#66d6d1", "portId":"lp2"},
            {"portColor":"#fae3d7", "portId":"lp3"},
            {"portColor":"#fae3d7", "portId":"lp4"},
            {"portColor":"#fae3d7", "portId":"lp5"},
            {"portColor":"#fae3d7", "portId":"lp6"},
            {"portColor":"#fae3d7", "portId":"lp7"},
            {"portColor":"#fae3d7", "portId":"lp8"},
          ], 
          "topArray":[ 
            {"portColor":"#d6effc", "portId":"top0"} 
          ], 
          "bottomArray":[ 
            {"portColor":"#eaeef8", "portId":"bp1"},
            {"portColor":"#eaeef8", "portId":"bp2"},
            {"portColor":"#6cafdb", "portId":"bp3"} 
          ], 
          "rightArray":[  
            {"portColor":"#6cafdb", "portId":"rp1"},
            {"portColor":"#6cafdb", "portId":"rp2"},
            {"portColor":"#66d6d1", "portId":"rp3"},
            {"portColor":"#fae3d7", "portId":"rp4"},
          ] 
        }, {
          "key":4, 
          "name":"EPS", 
          "loc":"100 300", 
          "size":"80 60", 
          "leftArray":[ 
            {"portColor":"#fae3d7", "portId":"left0"} 
          ], 
          "topArray":[ 
            {"portColor":"#6cafdb", "portId":"top0"} 
          ], 
          "bottomArray":[ 
            {"portColor":"#6cafdb", "portId":"bottom0"} 
          ], 
          "rightArray":[ 
            {"portColor":"#6cafdb", "portId":"c1tx"},
            {"portColor":"#66d6d1", "portId":"c2tx"} 
          ]
        }, {
          "key":5, 
          "name":"Q-Node 2", 
          "loc":"700 100", 
          "size":"80 80", 
          "leftArray":[ 
            {"portColor":"#eaeef8", "portId":"c1tx"},
            {"portColor":"#fadfe5", "portId":"c1rx"},
            {"portColor":"#eaeef8", "portId":"c2tx"},
            {"portColor":"#fadfe5", "portId":"c2rx"},
          ], 
          "topArray":[ 
            {"portColor":"#d6effc", "portId":"top0"} 
          ], 
          "bottomArray":[ 
            {"portColor":"#ebe3fc", "portId":"bottom0"} 
          ], 
          "rightArray":[ 
            {"portColor":"#fae3d7", "portId":"left0"} 
          ] 
        } ], 
        "linkDataArray": [ 
          {"from":4, "to":2, "fromPort":"c1tx", "toPort":"lp7"}, 
          {"from":4, "to":2, "fromPort":"c2tx", "toPort":"lp8"}, 
          {"from":1, "to":2, "fromPort":"c1tx", "toPort":"lp1"}, 
          {"from":1, "to":2, "fromPort":"c1rx", "toPort":"lp2"}, 
          {"from":1, "to":2, "fromPort":"c2tx", "toPort":"lp3"}, 
          {"from":1, "to":2, "fromPort":"c2rx", "toPort":"lp4"}, 
          {"from":5, "to":2, "fromPort":"c1tx", "toPort":"rp1"}, 
          {"from":5, "to":2, "fromPort":"c1rx", "toPort":"rp2"}, 
          {"from":5, "to":2, "fromPort":"c2tx", "toPort":"bp2"}, 
          {"from":5, "to":2, "fromPort":"c2rx", "toPort":"bp3"}, 
        ]
        */
      },
      currentNode: null,
      savedModelText: "",
      counter: 1,  // used by addNode
      counter2: 4  // used by modifyStuff
    };
  },
  mounted() {
    loader.load().then(function () {
      // Regular Map
      const myLatlng = new google.maps.LatLng(41.84141, -88.25352);
      const myLatlng2 = new google.maps.LatLng(41.71821, -87.97936);
      const mapOptions = {
        zoom: 12,
        //center: myLatlng,
        //scrollwheel: false, // we disable de scroll over the map, it is a really annoing when you scroll through page
        disableDefaultUI: true, // a way to quickly hide all controls
        zoomControl: true,
        styles: [
          {
            featureType: "administrative",
            elementType: "labels.text.fill",
            stylers: [{ color: "#888888" }],
          },
          {
            featureType: "landscape",
            elementType: "all",
            stylers: [{ color: "#f2f2f2" }],
          },
          {
            featureType: "poi",
            elementType: "all",
            stylers: [{ visibility: "off" }],
          },
          {
            featureType: "road",
            elementType: "all",
            stylers: [{ saturation: -100 }, { lightness: 45 }],
          },
          {
            featureType: "road.highway",
            elementType: "all",
            stylers: [{ visibility: "simplified" }],
          },
          {
            featureType: "road.arterial",
            elementType: "labels.icon",
            stylers: [{ visibility: "off" }],
          },
          {
            featureType: "transit",
            elementType: "all",
            stylers: [{ visibility: "off" }],
          },
          {
            featureType: "water",
            elementType: "all",
            stylers: [{ color: "#0E87CC" }, { visibility: "on" }],
          },
        ],
      };
      var map = new google.maps.Map(
        document.getElementById("map"),
        mapOptions
      );

      const marker = new google.maps.Marker({
        position: myLatlng,
        label: 'Q1',
        title: "Regular Map!",
        map: map,
      });

      const marker2 = new google.maps.Marker({
        position: myLatlng2,
        label: 'Q2',
        title: "Map2!",
        map: map,
      });

      const lineSymbol = {
        path: "M 0,-1 0,1",
        strokeOpacity: 1,
        scale: 4,
      };

      const path = new google.maps.Polyline({
        path: [myLatlng, myLatlng2],
        strokeColor: "#D3494E",
        strokeOpacity: 0,
        icons: [
          {
            icon: lineSymbol,
            offset: "0",
            repeat: "20px",
          },
        ],
        map: map,
      })

      var bounds = new google.maps.LatLngBounds();
      bounds.extend(marker.position);
      bounds.extend(marker2.position);

      map.fitBounds(bounds);
      var listener = google.maps.event.addListener(map, "idle", function () { 
        //map.setZoom(12); 
        google.maps.event.removeListener(listener); 
      });
    });
  },
};
</script>
<style></style>