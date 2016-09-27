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
    ready() {
      new Highcharts.StockChart({
        chart: {
          renderTo: 'container',
          events: {
            load() {
              const series = this.series[0];
              setInterval(() => {
                const x = (new Date()).getTime();
                const y = Math.round(Math.random() * 100);
                series.addPoint([x, y], true, true);
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
          }, {
            count: 10,
            type: 'minute',
            text: '10M'
          }, {
            count: 15,
            type: 'minute',
            text: '15M'
          }, {
            count: 30,
            type: 'minute',
            text: '30M'
          }, {
            count: 60,
            type: 'minute',
            text: '1H'
          }],
          inputEnabled: false,
          selected: 0
        },

        title: {
          text: 'MarketsWorld Live'
        },

        exporting: {
          enabled: false
        },

        series: [{
          name: 'Live data',
          data: (() => {
            const data = [];
            const time = (new Date()).getTime();

            for (let i = -999; i <= 0; i += 1) {
              data.push([
                time + i * 1000,
                Math.round(Math.random() * 100)
              ]);
            }
            return data;
          })()
        }]
      });
    }
  };
</script>
