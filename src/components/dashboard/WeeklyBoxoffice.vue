<template>
  <div>
    <span style="position: absolute; right: 20px"> </span>
    <base-title title="주간 박스오피스"></base-title>
    <v-row style="width: 100%" no-gutters class="mt-3">
      <v-col>
        <v-sheet class="mx-auto" elevation="8">
          <v-slide-group
            v-model="model"
            class="pa-4"
            show-arrows
          >
          <template v-slot:next>
            <p>{{right}}</p>
          </template>
              <template v-slot:prev>
            <p>{{left}}</p>
          </template>
            <v-slide-item v-for="n in 15" :key="n" v-slot="{ active, toggle }">
              <v-card
                :color="active ? undefined : 'grey lighten-1'"
                class="ma-4"
                height="200"
                width="100"
                @click="toggle"
              >
                <v-row class="fill-height" align="center" justify="center">
                  <v-scale-transition>
                    <v-icon
                      v-if="active"
                      color="black"
                      size="48"
                      v-text="'mdi-close-circle-outline'"
                    ></v-icon>
                  </v-scale-transition>
                </v-row>
                <p>제목</p>
              </v-card>
            </v-slide-item>
          </v-slide-group>
        </v-sheet>
      </v-col>
    </v-row>
  </div>
</template>
<script>
import { get } from "vuex-pathify";
import unitUtil from "@/utils/unitUtil";
export default {
  name: "ApCurrentStatus",
  data: () => {
    return {
      model: null,
      left: '<',
      right: '>',
      cardHeight: 200,
      apConnStatusValues: [],
      apRadioTypeValues: [],
      apRunTimeValues: [],
      pieOptions: {
        colors: ["#6fb5e3", "#ed6969"],
      },
      barLabeldOptions: {
        colors: ["#008ffb"],
      },
    };
  },
  watch: {
    zone() {
      this.refresh();
    },
    pageRefresh() {
      this.refresh();
    },
    dashboardRefresh() {
      this.refresh();
    },
  },
  computed: {
    pageRefresh: get("app/pageRefresh"),
    dashboardRefresh: get("app/dashboardRefresh"),
    tooltipFormatter() {
      return (value) => {
        return unitUtil.byteToUnit(value);
      };
    },
    legendFormatter() {
      return (name, value) => {
        return name + " (" + unitUtil.byteToUnit(value) + ")";
      };
    },
  },
  props: {
    zone: { type: String, default: "" },
  },
  methods: {
    refresh() {
      // this.getData();
    },
  },
  created() {
    this.refresh();
  },
  components: {},
};
</script>
<style scoped>

</style>