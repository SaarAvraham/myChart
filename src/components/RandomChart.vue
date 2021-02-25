<template>
    <div class="small">
        <doughnut-example :chart-data="datacollection"></doughnut-example>
        <button @click="fillData()">Randomize</button>
    </div>
</template>

<script>
    import DoughnutExample from "@/components/DoughnutExample";

    export default {
        components: {
            DoughnutExample
        },
        data() {
            return {
                datacollection: null
            }
        },
        mounted() {
            this.fillData()
        },
        methods: {
            fillData() {
                this.datacollection = {
                    labels: ['Successfully Deleted', 'Partially Deleted', 'Failed to Delete', 'Unproccessed'],
                    datasets: [
                        {
                            labels: ['Successfully Deleted', 'Partially Deleted', 'Failed to Delete', 'Unproccessed'],
                            backgroundColor: [
                                '#41b883',
                                '#fcf205',
                                '#DD1B16',
                                '#828282' +
                                ''
                            ],
                            data: [this.getRandomInt(), this.getRandomInt(), this.getRandomInt(), this.getRandomInt()]
                        }
                    ]
                }
            },
            getRandomInt() {
                return Math.floor(Math.random() * (50 - 5 + 1)) + 5
            }
        }
    }
</script>

<style>
    .small {
        max-width: 600px;
        margin: 150px auto;
    }
</style>