<template>
  <div class="page-container">
    <md-app>
      <md-app-toolbar class="md-primary">
        <span class="md-title">Covid-19 Tracker</span>
      </md-app-toolbar>
      <md-app-content>
        <Cards :stats="stats"/>
        <Chart/>
      </md-app-content>
    </md-app>
  </div>
</template>
<script>
import Cards from "./components/Cards";
import Chart from "./components/Chart";
import { baseUrl } from "./consts/index";
export default {
  name: "App",
  components: {
    Cards,
    Chart
  },
  data() {
    return {
      stats: {
        confirmed: {
          title: "Infected",
          description: "Number of active cases of COVID-19."
        },
        recovered: {
          title: "Recovered",
          description: "Number of recoveries from COVID-19."
        },
        deaths: {
          title: "Deaths",
          description: "Number of deaths caused by COVID-19"
        },
        lastUpdate: ""
      }
    };
  },

  mounted() {
    this.$http.get(baseUrl).then(({ data }) => {
      this.stats = Object.keys(this.stats).reduce((acc, key) => {
        acc[key] =
          typeof acc[key] === "object"
            ? { ...acc[key], ...data[key] }
            : data[key];
        return acc;
      }, this.stats);
    });
  }
};
</script>

<style lang="scss" scoped>
.md-app {
  margin: 0;
  border: 1px solid rgba(#000, 0.12);
}
</style>
