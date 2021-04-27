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
            <template v-slot:header>
              <h3 class="mb-0">System Topology</h3>
            </template>

            <diagram ref="diag"
              v-bind:model-data="diagramData"
              style="border:solid 1px black; width:100%; height:600px">
            </diagram>

          </card>
        </div>

        <!--
        <div class="col-lg-6">
          <card shadow gradient="default" header-classes="bg-transparent">
            <template v-slot:header>
              <h3 class="mb-0 text-white">Dark timeline</h3>
            </template>
            <time-line type="one-side">
              <time-line-item badge-type="success" badge-icon="ni ni-bell-55">
                <small class="text-light font-weight-bold">10:30 AM</small>
                <h5 class="text-white mt-3 mb-0">New message</h5>
                <p class="text-light text-sm mt-1 mb-0">
                  Nullam id dolor id nibh ultricies vehicula ut id elit. Cum
                  sociis natoque penatibus et magnis dis parturient montes,
                  nascetur ridiculus mus.
                </p>
                <div class="mt-3">
                  <badge rounded type="success">design</badge>&nbsp;
                  <badge rounded type="success">system</badge>&nbsp;
                  <badge rounded type="success">creative</badge>
                </div>
              </time-line-item>

              <time-line-item badge-type="danger" badge-icon="ni ni-html5">
                <small class="text-light font-weight-bold">10:30 AM</small>
                <h5 class="text-white mt-3 mb-0">Product issue</h5>
                <p class="text-light text-sm mt-1 mb-0">
                  Nullam id dolor id nibh ultricies vehicula ut id elit. Cum
                  sociis natoque penatibus et magnis dis parturient montes,
                  nascetur ridiculus mus.
                </p>
                <div class="mt-3">
                  <badge rounded type="danger">design</badge>&nbsp;
                  <badge rounded type="danger">system</badge>&nbsp;
                  <badge rounded type="danger">creative</badge>
                </div>
              </time-line-item>

              <time-line-item badge-type="info" badge-icon="ni ni-like-2">
                <small class="text-light font-weight-bold">10:30 AM</small>
                <h5 class="text-white mt-3 mb-0">New likes</h5>
                <p class="text-light text-sm mt-1 mb-0">
                  Nullam id dolor id nibh ultricies vehicula ut id elit. Cum
                  sociis natoque penatibus et magnis dis parturient montes,
                  nascetur ridiculus mus.
                </p>
                <div class="mt-3">
                  <badge rounded type="info">design</badge>&nbsp;
                  <badge rounded type="info">system</badge>&nbsp;
                  <badge rounded type="info">creative</badge>
                </div>
              </time-line-item>

              <time-line-item badge-type="success" badge-icon="ni ni-bell-55">
                <small class="text-light font-weight-bold">10:30 AM</small>
                <h5 class="text-white mt-3 mb-0">New message</h5>
                <p class="text-light text-sm mt-1 mb-0">
                  Nullam id dolor id nibh ultricies vehicula ut id elit. Cum
                  sociis natoque penatibus et magnis dis parturient montes,
                  nascetur ridiculus mus.
                </p>
                <div class="mt-3">
                  <badge rounded type="success">design</badge>&nbsp;
                  <badge rounded type="success">system</badge>&nbsp;
                  <badge rounded type="success">creative</badge>
                </div>
              </time-line-item>

              <time-line-item badge-type="danger" badge-icon="ni ni-html5">
                <small class="text-light font-weight-bold">10:30 AM</small>
                <h5 class="text-white mt-3 mb-0">Product issue</h5>
                <p class="text-light text-sm mt-1 mb-0">
                  Nullam id dolor id nibh ultricies vehicula ut id elit. Cum
                  sociis natoque penatibus et magnis dis parturient montes,
                  nascetur ridiculus mus.
                </p>
                <div class="mt-3">
                  <badge rounded type="danger">design</badge>&nbsp;
                  <badge rounded type="danger">system</badge>&nbsp;
                  <badge rounded type="danger">creative</badge>
                </div>
              </time-line-item>
            </time-line>
          </card>
        </div>
        -->

      </div>
    </div>
  </div>
</template>
<script>
//import TimeLine from "@/components/Timeline/TimeLine";
//import TimeLineItem from "@/components/Timeline/TimeLineItem";
import RouteBreadcrumb from "@/components/Breadcrumb/RouteBreadcrumb";
import BaseHeader from "@/components/BaseHeader";
//import Badge from "@/components/Badge";

import Diagram from "@/components/Diagram";

export default {
  components: {
    //Badge,
    BaseHeader,
    //TimeLine,
    //TimeLineItem,
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
          "name":"Switch 1", 
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
            {"portColor":"#6cafdb", "portId":"rp0"},
            {"portColor":"#6cafdb", "portId":"rp1"},
            {"portColor":"#66d6d1", "portId":"rp2"},
            {"portColor":"#fae3d7", "portId":"rp3"},
          ] 
        }, {
          "key":3, 
          "name":"Switch 2", 
          "loc":"500 200", 
          "size":"80 180", 
          "leftArray":[ 
            {"portColor":"#6cafdb", "portId":"lp0"},
            {"portColor":"#6cafdb", "portId":"lp1"},
            {"portColor":"#66d6d1", "portId":"lp2"},
            {"portColor":"#fae3d7", "portId":"lp3"},
          ], 
          "topArray":[ 
            {"portColor":"#66d6d1", "portId":"top0"} 
          ], 
          "bottomArray":[ 
            {"portColor":"#6cafdb", "portId":"bottom0"} 
          ], 
          "rightArray":[  
            {"portColor":"#6cafdb", "portId":"rp0"},
            {"portColor":"#6cafdb", "portId":"rp1"},
            {"portColor":"#66d6d1", "portId":"rp2"},
            {"portColor":"#fae3d7", "portId":"rp3"},
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
        } ], 
        "linkDataArray": [ 
          {"from":4, "to":2, "fromPort":"c1tx", "toPort":"lp7"}, 
          {"from":4, "to":2, "fromPort":"c2tx", "toPort":"lp8"}, 
          {"from":2, "to":3, "fromPort":"rp0", "toPort":"lp2"}, 
          {"from":2, "to":3, "fromPort":"rp1", "toPort":"lp3"}, 
          {"from":1, "to":3, "fromPort":"c1tx", "toPort":"rp1"}, 
          {"from":1, "to":3, "fromPort":"c1rx", "toPort":"rp2"}, 
          {"from":1, "to":2, "fromPort":"c2tx", "toPort":"lp3"}, 
          {"from":1, "to":2, "fromPort":"c2rx", "toPort":"lp4"}, 
        ]
      },
      currentNode: null,
      savedModelText: "",
      counter: 1,  // used by addNode
      counter2: 4  // used by modifyStuff
    };
  },
};
</script>
<style></style>