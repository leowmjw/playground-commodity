<style scoped>

    .node-card {
        background-color: #00d4b4;
    }

    .node-alive {
        background-color: yellowgreen;
    }

    .node-dead {
        background-color: red;
    }

</style>

<template>

    <div class="node-card">
        <div :class="(liveliness == 'alive') ? 'node-alive' : 'node-dead' ">
            <h2>State: {{ state }}</h2>
            <div>
                <h3>PIR</h3>
                {{ data.pir }}
            </div>
            <div>
                <h3>DOOR</h3>
                {{ data.door }}
            </div>
        </div>
        <div>
            RAW: {{ (raw == null || raw == undefined ) ? '' : raw | json }}
            <button @click="refreshData()">{{ (liveliness == 'alive' ? 'Disarm' : 'Arm') }}</button>
        </div>
    </div>

</template>

<script>

    import util from 'util'
    // Actual subcomponents neede below ..

    // Actual libs needed below ...

    export default {
        props: ['influxdb', 'slot'],
        components: {},
        watch: {},
        events: {
            'new-data': function (type, mydata) {
                // New data comes in ... from parent compoenent ...
                console.error("NEW DATA TYPE: %s .... %s", type, util.inspect(mydata, {depth: 10}))
                this.data = mydata
            }
        },
        data () {
            return {
                // Liveliness: Alive . DEAD
                liveliness: "alive",
                // State: Normal Business Hour; After Business Hour
                state: "normal",
                // Alarm: Powered on; Disabled ... only show when state is "night"
                alarm: null,
                // Data: Split by type; per minute; last n minutues per segment?? Last m segments??
                data: {
                    "pir": null,
                    "door": null
                },
                raw: null
            }
        },
        ready () {

        },
        methods: {
            refreshData () {
                console.error("In refreshData ..")
                if (this.liveliness == "alive") {
                    this.liveliness = "dead"
                } else {
                    this.liveliness = "alive"

                }
                /*
                 if (this.influxdb == null || this.influxdb == undefined) {
                 console.error("Nothing to Do ...")
                 } else {
                 this.influxdb.query("show databases", function (err, results) {
                 console.error("ERROR: ", err)
                 console.error("RESULT: ", util.inspect(results, {depth: 10}))
                 })
                 }
                 */
            }
        },
        computed: {}
    }

</script>