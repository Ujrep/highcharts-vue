<style lang="scss">
  @import 'app/common/utils/colors.scss';
  @import 'app/common/utils/media.scss';

  .Home {
    height: 100%;

    text-align: center;

  }

  .Home-container {
    margin: 0 20px;

    @include media(medium) {
      // margin: 0 50px;
    }

    @include media(large) {
      max-width: 1170px;
      margin: 0 auto;
    }
  }
</style>

<template>

  <div class="Home">
    <div class="Home-container">
      <custom-header>

      </custom-header>

      <div id="container" style="min-width: 310px; height: 400px; margin: 0 auto"></div>
    </div>
  </div>

</template>

<script>
  import Header from 'components/partials/header.vue';

  import Highcharts from 'highcharts/highstock';

  export default {
    name: 'Home',
    data() {
      return {
      };
    },
    components: {
      'custom-header': Header
    },
    methods: {
      prettyDate() {
        const monthNames = [
          'January', 'February', 'March',
          'April', 'May', 'June', 'July',
          'August', 'September', 'October',
          'November', 'December'
        ];

        const date = new Date();
        const day = date.getDate();
        const monthIndex = date.getMonth();
        const year = date.getFullYear();

        return day + ' ' + monthNames[monthIndex] + ' ' + year;
      }
    },
    ready() {
      Highcharts.setOptions({
        global: {
          useUTC: false
        }
      });

      const chart = new Highcharts.Chart({
        chart: {
          renderTo: 'container',
          events: {
            load() {
              const series = this.series[0];
              setInterval(() => {
                const x = new Date();
                const y = Math.round(Math.random() * 10);
                // series.addPoint([x, y], true, true);
              }, 500);
            }
          }
        },

        rangeSelector: {
          buttons: [{
            count: 1,
            type: 'minute',
            text: '1M'
          }, {
            count: 5,
            type: 'minute',
            text: '5M'
          }],
          inputEnabled: false,
          selected: 0
        },

        title: {
          text: 'Live random data'
        },

        exporting: {
          enabled: false
        },

        series: [{
          name: 'Random data',
          data: (() => {
            const data = [];
            // const time = new Date();

            for (let i = 0; i <= 10; i += 1) {
              const point = [
                this.prettyDate(),
                Math.round(Math.random() * 10)
              ];
              data.push(point);
            }
            return data;
          })()
        }]
      });
      console.log(chart);
    }
  };
</script>
