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
              <h3 class="mb-0">Q-Net Teleportation Service</h3>
            </template>

          </card>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import RouteBreadcrumb from "@/components/Breadcrumb/RouteBreadcrumb";
import BaseHeader from "@/components/BaseHeader";
//import Badge from "@/components/Badge";


export default {
  components: {
    BaseHeader,
    RouteBreadcrumb,
  },
  data() {
  },
};
</script>
<style></style>