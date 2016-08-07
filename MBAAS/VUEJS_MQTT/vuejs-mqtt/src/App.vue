<style>
    body {
        font-family: Helvetica, sans-serif;
        padding-top: 70px;
        /*
           Required padding for .navbar-fixed-top.
           Remove if using .navbar-static-top. Change if height of navigation changes.
        */
    }

    footer {
        margin: 50px 0;
    }

    .thing {
        padding-top: 2em;
    }

    .thingheat {
        padding-top: 2em;
    }

</style>

<template>
    <div id="app">
        <h2>{{ msg }}</h2>

        <navigation></navigation>

        <div class="container">

            <div class="row thing">
                <h3>Ninja Nodes</h3>
                <div class="col-md-3">
                    <things slot="1"></things>
                    <things slot="2"></things>
                </div>
                <div class="col-md-3">
                    <things slot="3"></things>
                    <things slot="4"></things>
                </div>
                <div class="col-md-3">
                    <things slot="5"></things>
                    <things slot="6"></things>
                </div>
                <div class="col-md-3">
                    <things slot="7"></things>
                    <things slot="8"></things>
                </div>
            </div>
            <div class="row thingheat">
                <thingsdataheatmap></thingsdataheatmap>
            </div>

            <hr>

            <footer>Ninja Sensors 2016</footer>
        </div>

    </div>

</template>

<script>

    // For debugging only ..
    import util from 'util'
    // Actual subcomponents used
    import Navigation from './components/Navigation.vue'
    import Things from './components/Things.vue'
    import ThingsDataHeatMap from './components/ThingsDataHeatMap.vue'

    export default {
        components: {
            navigation: Navigation,
            things: Things,
            thingsdataheatmap: ThingsDataHeatMap
        },
        data () {
            return {
                // note: changing this line won't causes changes
                // with hot-reload because the reloaded component
                // preserves its current state and we are modifying
                // its initial state.
                msg: 'TheThingsNetwork Store with Ninja Detector',
                influxdb: null
            }
        },
        ready() {

            // Socket.io readiness ..
            const socket = io('http://106.186.17.6:8080')
            socket.on('uplink', function (mydata) {
                // Log to the console
                console.error("Uplink from Device:" + mydata.devEUI)
                // Create a new DOM element
                // var uplink = document.createElement("div")
                // var date = new Date(data.metadata.server_time)
                // var dateString = date.getHours() + ":" + date.getMinutes() + ":" + date.getSeconds()
                // uplink.innerText = dateString + " - Uplink " + data.counter + " from " + data.devEUI + ": " + JSON.stringify(data.fields)
                // Append to the activity feed
                // activityFeed.appendChild(uplink)
                this.$broadcast('new-data', 'alive', mydata)

            }.bind(this))
            socket.on('activation', function (data) {
                // Log to the console
                console.error("Activated Device:" + data.devEUI, data)
                // Create a new DOM element
                // var activation = document.createElement("div")
                // activation.innerText = "Activated " + data.devEUI
                // Append to the activity feed
                // activityFeed.appendChild(activation)
            })

            // Get InfluxDB client ready??
            // const influx = require('influx')
            /*
             const client = influx({
             host : '106.186.17.6',
             database: 'mydb'
             })

             this.influxdb = client
             */

            // Above does not work :( Simulate data coming in
            const mydata = {
                pir: "123",
                door: "555"
            }
            this.$broadcast('new-data', 'alive', mydata)

        }
    }
</script>

