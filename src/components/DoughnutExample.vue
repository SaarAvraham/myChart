<!--<template>-->
<!--    -->
<!--</template>-->

<script>
    import { Doughnut, mixins } from 'vue-chartjs'
    import ChartJsPluginDataLabels from 'chartjs-plugin-datalabels'
    const { reactiveProp } = mixins
    import Chart from 'chart.js'
    Chart.plugins.register({
        ChartJsPluginDataLabels
    });

    Chart.helpers.merge(Chart.defaults.global.plugins.datalabels, {
        color: '#000000'
    });

    export default {
        extends: Doughnut,
        mixins: [reactiveProp],
        name: "DoughnutExample",
        mounted () {
            // this.chartData is created in the mixin.
            // If you want to pass options please create a local options object
            this.renderChart(this.chartData, this.options)
        }
    }
</script>

<style scoped>
</style>