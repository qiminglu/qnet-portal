<template>
  <div>
    <base-header class="pb-6">
      <div class="row align-items-center py-4">
        <div class="col-lg-6 col-7">
          <h6 class="h2 text-white d-inline-block mb-0">Site Administration </h6>
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
      <div class="row card-wrapper">
        <div class="col-lg-4">

          <!-- Basic with card header -->
          <card>
            <template v-slot:header>
              <h5 class="h3 mb-0">
                Q-NetARCH Server Configuration
              </h5>
            </template>
            <p class="card-text mb-4">
              Administrators can configure the backend details used for the Q-NetArch
              Web Portal. Following items can be configured,
            </p>

            <ul class="list-unstyled my-4">
              <li style="margin-bottom:15px">
                <div class="d-flex align-items-center">
                  <div>
                    <div class="icon icon-xs icon-shape bg-white text-primary shadow rounded-circle" >
                      <i class="fas fa-terminal"></i>
                    </div>
                  </div>
                  <div>
                    <span class="pl-2 text-sm"
                      >MongoDB server</span
                    >
                  </div>
                </div>
              </li>

              <li style="margin-bottom:15px">
                <div class="d-flex align-items-center">
                  <div>
                    <div class="icon icon-xs icon-shape bg-white text-primary shadow rounded-circle" >
                      <i class="fas fa-pen-fancy"></i>
                    </div>
                  </div>
                  <div>
                    <span class="pl-2 text-sm"
                      >Mosquitto MQTT broker</span
                    >
                  </div>
                </div>
              </li>

              <li style="margin-bottom:15px">
                <div class="d-flex align-items-center">
                  <div>
                    <div class="icon icon-xs icon-shape bg-white text-primary shadow rounded-circle" >
                      <i class="fas fa-hdd"></i>
                    </div>
                  </div>
                  <div>
                    <span class="pl-2 text-sm"
                      >Node.js API server</span
                    >
                  </div>
                </div>
              </li>
 
              <li style="margin-bottom:15px">
                <div class="d-flex align-items-center">
                  <div>
                    <div class="icon icon-xs icon-shape bg-white text-primary shadow rounded-circle" >
                      <i class="fas fa-cloud"></i>
                    </div>
                  </div>
                  <div>
                    <span class="pl-2 text-sm">
                      Site certificates</span
                    >
                  </div>
                </div>
              </li>
 
            </ul>
 
            <router-link to="/empty">
              <base-button type="warning" class="btn btn-primary" >
                <i class="fas fa-exclamation-triangle"></i>&nbsp; Server Configuration
              </base-button>
            </router-link>
          </card>



        </div>

        <div class="col-lg-4">

          <card gradient="default">
            <h3 class="card-title text-white">Q-Node

            </h3>
            <blockquote class="blockquote text-white mb-0">
              <p>
                List and manage all availabe Q-Nodes in the system. Including the 
                channels, wavelength, and others.
              </p>

              <router-link to="/empty">
              <p class="text-white float-right">Click to Enter ></p>
              </router-link>

            </blockquote>
          </card>

          <card gradient="primary">
            <h3 class="card-title text-white">EPS</h3>
            <blockquote class="blockquote text-white mb-0">
              <p>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer
                posuere erat a ante.
              </p>

              <router-link to="/empty">
              <p class="text-white float-right">Click to Enter ></p>
              </router-link>

            </blockquote>
          </card>


        </div>


        <div class="col-lg-4">

          <card gradient="warning">
            <h3 class="card-title text-white">BSM Station</h3>
            <blockquote class="blockquote text-white mb-0">
              <p>
                Lorem ipsum dolor sit amet, consectetur adipiscing elit. Integer
                posuere erat a ante.
              </p>

              <router-link to="/empty">
              <p class="text-white float-right">Click to Enter ></p>
              </router-link>

            </blockquote>
          </card>
 

          <card gradient="info">
            <h3 class="card-title text-white">SDN</h3>
            <blockquote class="blockquote text-white mb-0">
              <p>
                Manage the SDN controller and network topology in the system.
              </p>

              <router-link to="/empty">
              <p class="text-white float-right">Click to Enter ></p>
              </router-link>

            </blockquote>
          </card>


        </div>

      </div>
    </div>
  </div>
</template>
<script>
import RouteBreadcrumb from "@/components/Breadcrumb/RouteBreadcrumb";
import BaseHeader from "@/components/BaseHeader";
import StatsCard from "@/components/Cards/StatsCard";

export default {
  components: {
    BaseHeader,
    RouteBreadcrumb,
    StatsCard,
  },
};
</script>
<style></style>
