<template>
    <div>
        <RandomChart></RandomChart>
        <p v-for="message in messages" :key="message">{{ message }}</p>
    </div>
</template>

<script>
    // We store the reference to the SSE object out here
    // so we can access it from other methods
    import RandomChart from "@/components/RandomChart";
    let msgServer;

    // import Vue from 'vue'

    // import { Doughnut } from 'vue-chartjs'


    export default {
        name: 'sse-test',
        components: {RandomChart},
        data() {
            return {
                messages: [],
            };
        },
        mounted() {
            // console.log("dsads")
            // Vue.axios.get(api).then((response) => {
            //     console.log(response.data)
            // })

            this.$sse('http://localhost:8081/stream-sse', ) // or { format: 'plain' }
                .then(sse => {
                    // Store SSE object at a higher scope
                    msgServer = sse;

                    // Catch any errors (ie. lost connections, etc.)
                    sse.onError(e => {
                        console.error('lost connection; giving up!', e);

                        // This is purely for example; EventSource will automatically
                        // attempt to reconnect indefinitely, with no action needed
                        // on your part to resubscribe to events once (if) reconnected
                        sse.close();
                    });

                    // Listen for messages without a specified event
                    // eslint-disable-next-line no-unused-vars
                    sse.subscribe('', (message, rawEvent) => {
                        console.log(message)
                        console.warn('Received a message w/o an event!', message);
                    });

                    // // Listen for messages based on their event (in this case, "chat")
                    // // eslint-disable-next-line no-unused-vars
                    // sse.subscribe('chat', (message, rawEvent) => {
                    //     console.log(message)
                    //
                    //     this.messages.push(message);
                    // });
                })
                .catch(err => {
                    // When this error is caught, it means the initial connection to the
                    // events server failed.  No automatic attempts to reconnect will be made.
                    console.error('Failed to connect to server', err);
                });
        },
        beforeDestroy() {
            // Make sure to close the connection with the events server
            // when the component is destroyed, or we'll have ghost connections!
            msgServer.close();
        },
    };
</script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
    }

    li {
        display: inline-block;
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>
