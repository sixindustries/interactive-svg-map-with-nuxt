<template>
  <div>
    <v-app-bar 
      app 
      color="white" 
      :height="$vuetify.breakpoint.mdAndUp ? '100' : '70'" 
      class="px-md-10"
      elevate-on-scroll
      >
      <span class="text-h5 text-sm-h3">Nuxt Interactive SVG Map</span>
    </v-app-bar>

    <v-container fluid>
      <v-row justify="center" align="center" class="grey lighten-4 py-10 py-md-15">     
        <v-col cols="12" md="7" class="text-center">
          <radio-svg-map v-model="selectedLocation" :map="USA" @click.prevent="determineState()" />
        </v-col>
        <v-col cols="10" sm="6" md="4" lg="3" xl="2" class="text-center">          
          <v-card class="pa-10 elevation-6 rounded-lg">
            <v-row justify="center" align="center">
              <span>Your Selection:</span>
              <span v-if="!selectedLocation" class="primary--text ml-2">Choose from the map</span>
              <span class="primary--text ml-2">{{ locationDisplay }}</span>
            </v-row>
          </v-card>       
        </v-col>
      </v-row>      
    </v-container>
  </div>
</template>


<script>
import { RadioSvgMap } from "vue-svg-map";
import USA from "@svg-maps/usa";

export default {
  components: {
    RadioSvgMap
  },

  // ~~~~~~~~~~~~~~~~~~ DATA ~~~~~~~~~~~~~~~~~~~
  data() {
    return {
      USA,
      selectedLocation: null,
      locationDisplay: "",
    };
  },

  // ~~~~~~~~~~~~~~~~~~ PROPERTIES ~~~~~~~~~~~~~~~~~~~
  computed: {
    
  },

  watch: {},

  // ~~~~~~~~~~~~~ HOOKS ~~~~~~~~~~~~~~~~~
  mounted() {},

  updated() {},

  // ~~~~~~~~~~~~~~~~~~  METHODS ~~~~~~~~~~~~~~~~~~~
  methods: {
    determineState() {
      this.USA.locations.forEach(item => {
        if (item.id === this.selectedLocation) {
          return this.locationDisplay = item.name;     
        }
        return null;
      })  
    }
  }
};
</script>

<style>
.svg-map {
  width: 100%;
  height: auto;
  stroke: #fff;
  stroke-width: 1;
  stroke-linecap: round;
  stroke-linejoin: round; }
  .svg-map__location {
    fill: #bbb;
    cursor: pointer; }
    .svg-map__location:focus, .svg-map__location:hover {
      fill: #ccc;
      outline: 0; }
    .svg-map__location[aria-checked="true"] {
      fill: #007dc3; }
</style>
