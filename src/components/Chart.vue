
<script>
import { dailyDataUrl } from "./../consts/index";
import { Line } from "vue-chartjs";
export default {
  name: "Chart",
  extends: Line,
  mounted() {
    this.$http.get(dailyDataUrl).then(({ body }) => {
      console.log(body);
      let chartdata = {
        labels: body.map(({ reportDate }) => reportDate),
        datasets: [
          {
            label: "Infected",
            data: body.map(({ totalConfirmed }) => totalConfirmed),
            backgroundColor: "#f87979"
          }
        ]
      };
      let options = {
        responsive: true,
        maintainAspectRatio: false
      };
      this.renderChart(chartdata, options);
    });
  }
};
</script>

