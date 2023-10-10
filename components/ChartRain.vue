<template>
  <div>
    <apexchart height="200" type="bar" :options="chartOptionsRain" :series="chartDataRain" />
  </div>
</template>

<script>
export default {
  data() {
    return {
      chartOptionsRain: {
        chart: {
          type: 'bar',
          toolbar: {
            show: false
          },
        },
        plotOptions: {
          bar: {
            borderRadius: 10,
            dataLabels: {
              position: 'top', // top, center, bottom
            },
          }
        },
        dataLabels: {
          enabled: true,
          formatter: function (val) {
            return val + "mm";
          },
          offsetY: -20,
          style: {
            fontSize: '8px',
            colors: ["#304758"]
          }
        },
        xaxis: {
          categories: [],
          position: 'top',
          axisBorder: {
            show: false
          },
          axisTicks: {
            show: false
          },
          crosshairs: {
            fill: {
              type: 'gradient',
              gradient: {
                colorFrom: '#D8E3F0',
                colorTo: '#BED1E6',
                stops: [0, 50],
                opacityFrom: 0.4,
                opacityTo: 0.5,
              }
            }
          },
          tooltip: {
            enabled: true,
          }
        },
        yaxis: {
          axisBorder: {
            show: false
          },
          axisTicks: {
            show: false,
          },
          labels: {
            show: false,
            formatter: function (val) {
              return val + "mm";
            }
          }

        }
      },
      chartDataRain: [],
    };
  },
  async mounted() {
    const response = await fetch('https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&hourly=rain&past_days=1&forecast_days=1');
    const data = await response.json();
    this.chartOptionsRain = {
      xaxis: {
        categories: data.hourly.time.map(function (time) {
          return time.split("T")[1];
        }),
      },
    };

    this.chartDataRain = [
      {
        name: 'Rain',
        data: data.hourly.rain,
      },
    ];
  },
};
</script>