<template>
  <div>
    <!-- Card Timeline-->
    <h1>Agenda de reservas</h1>
    <div class="card mx-auto">
      <div>
        <!--Timeline-->
        <div class="mx-10" id="visualization">
          <div class="menu">
            <input
              style="display: none"
              id="sliderZoom"
              type="range"
              class="range"
              name="a"
              min="-1"
              max="1"
              step="0.1"
              value="0"
            />
          </div>
            <button @click="moveLeft()" color="secondary" class="arrow-left">
          <i class="white--text">mdi-chevron-left</i>
        </button>
        <button @click="moveRight()" color="secondary" class="arrow-right">
          <i class="white--text">mdi-chevron-right</i>
        </button>
  
        </div>
      
        </div>
    </div>
 </div>
        <!-- End Timeline -->
     
   
   
 
</template>

<script>
import Vue from "vue";
import moment from "@/plugins/moment";
import vis from "@/plugins/vis";

Vue.use(vis);

export default {
  props: {
    items: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {
      // vis
      container: "",
      reservas: [],
      defaultItem: {
        content: "Reserva #",
        start: "",
        end: "",
      },
    };
  },
  mounted() {
  },
  methods: {
    resetTimeline() {
      this.timeline.destroy();
    },

    renderTimeline() {
      if(this.timeline){
        this.resetTimeline
      }
      // Vis
      this.container = document.getElementById("visualization");
      this.options = {
        //stack: false,
        orientation: {
          axis: "top",
          item: "top",
        },
        //zoomMax: 31536000000, // just one year
        zoomMax: 87600900, // 10,000 years is maximum possible
        zoomMin: 10000000, // 10ms
      };
      this.timeline = new vis.Timeline(
        this.container,
        this.reservas,
        this.options
      );
      /**
       * Move the timeline a given percentage to left or right
       * @param {Number} percentage   For example 0.1 (left) or -0.1 (right)
       */

      // Using slider to zoomIn or zoomOut
      document
        .getElementById("sliderZoom")
        .addEventListener("input", function () {
          var value = this.value;
          if (value < 0) {
            let start = moment().year(moment().year() - 100000), // to adjust with options
              end = moment().year(moment().year() + 1);
            this.timeline.zoomOut(-value);
            if (value === "-1") this.timeline.setWindow(start, end);
          } else if (value > 0) {
            let start = moment(),
              end = moment(moment().utc() + 10);
            this.timeline.zoomIn(value);
            if (value === "1") this.timeline.setWindow(start, end);
          } else {
            this.timeline.fit(this.items.getIds());
            this.value = 0;
          }
        });
    },

    resetZoom() {
      // To reset zoom initial state
      document.getElementById("fit").onclick = function () {
        //$('.range').next().text('0'); // set default if to use output with input range
        document.getElementById("sliderZoom").value = 0;
        this.timeline.fit(this.items.getIds());
      };
    },
    move(percentage) {
      let range = this.timeline.getWindow();
      let interval = range.end - range.start;
      this.timeline.setWindow({
        start: range.start.valueOf() - interval * percentage,
        end: range.end.valueOf() - interval * percentage,
      });
    },

    moveLeft() {
      return this.move(0.3);
    },
    moveRight() {
      return this.move(-0.3);
    },
  },
  watch: {
    items() {
      this.reservas = new vis.DataSet(this.items);
      if (this.timeline) {
        this.resetTimeline();
      }
      this.renderTimeline();
    },
  },
  created() {},
};
</script>

<style scoped>
@import "../../styles/style.css";
@import "../../styles/full-style.css";


</style>
