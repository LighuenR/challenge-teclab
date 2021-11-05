<template>
  <div>
    <!-- Card Timeline-->
    <h3>Agenda de reservas</h3>
    <div>
      <div>
        <!--Timeline-->
        <div id="visualization">
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
        </div>
        <div class="botones">
          <button @click="moveLeft()" color="secondary" class="arrow-left">
            <i class="fas fa-chevron-left"></i>
          </button>
          <button @click="moveRight()" color="secondary" class="arrow-right">
            <i class="fas fa-chevron-right"></i>
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
    this.container = document.getElementById("visualization");
    this.reservas = new vis.DataSet(this.items);
    if (!this.container) return;
    this.renderTimeline();
  },
  methods: {
    resetTimeline() {
      this.timeline.destroy();
    },

    renderTimeline() {
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
      return this.move(1);
    },
    moveRight() {
      return this.move(-1);
    },
  },
  watch: {
    items() {
      this.reservas = new vis.DataSet(this.items);
      console.log(this.reservas, "Reservas");
      if (this.timeline) {
        this.resetTimeline();
      }
      this.renderTimeline();
    },
  },
};
</script>

<style scoped>
@import "../../styles/style.css";
@import "../../styles/full-style.css";

h3 {
  text-align: start;
}
.botones {
  padding: 1rem;
}
.botones button {
  padding:0.5rem 1rem;
  margin: 0 1rem;
  background: white;
  border-radius: 4px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.4);
  border:none;
}
</style>
