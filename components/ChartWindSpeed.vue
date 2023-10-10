<template>
  <div>
    <apexchart height="200" type="line" :options="chartOptionsWindSpeed" :series="chartDataWindSpeed" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      chartOptionsWindSpeed: {
        chart: {
          type: 'line',
          toolbar: {
            show: false
          },
        },
        stroke: {
          curve: 'stepline',
          width: 2
        },
        dataLabels: {
          enabled: false
        },
        markers: {
          hover: {
            sizeOffset: 4
          }
        },
        xaxis: {},
        tooltip: {
          y: {
            formatter: function (value) {
              return value.toLocaleString() + 'm';
            }
          }
        },
      },
      chartDataWindSpeed: [],
    };
  },
  async mounted() {
    const response = await fetch('https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&hourly=windspeed_10m&past_days=1&forecast_days=1');
    const data = await response.json();
    this.chartOptionsWindSpeed = {
      xaxis: {
        categories: data.hourly.time.map(function (time) {
          return time.split("T")[1];
        }),
      },
    };

    this.chartDataWindSpeed = [
      {
        name: 'Wind Speed',
        data: data.hourly.windspeed_10m,
      },
    ];
  },
};
</script>