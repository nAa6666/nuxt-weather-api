<template>
  <div>
    <apexchart height="200" type="area" :options="chartOptions" :series="chartData" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      chartOptions: {
        chart: {
          type: 'area',
          toolbar: {
            show: false
          },
        },
        dataLabels: {
          enabled: false
        },
        markers: {
          size: 0,
        },
        xaxis: {},
        tooltip: {
          y: {
            formatter: function (value) {
              return value.toLocaleString() + '°C';
            }
          }
        },
      },
      chartData: [],
    };
  },
  async mounted() {
    const response = await fetch('https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&hourly=temperature_2m&past_days=1&forecast_days=1');
    const data = await response.json();
    this.chartOptions = {
      xaxis: {
        categories: data.hourly.time.map(function (time) {
          return time.split("T")[1];
        }),
      },
    };

    this.chartData = [
      {
        name: 'Temperature',
        data: data.hourly.temperature_2m,
      },
    ];
  },
};
</script>