<style scoped>
</style>

<template>
    <div>
        <h3>PIR</h3>
        {{ data.pir }}
    </div>
    <div>
        <h3>DOOR</h3>
        {{ data.door }}
    </div>
    <div>
        RAW: {{ (raw == null || raw == undefined ) ? '' : raw | json }}
        <button @click="refreshData()">Refresh</button>
    </div>
</template>

<script>

    import util from 'util'
    // Actual subcomponents neede below ..

    // Actual libs needed below ...

    export default {
        props: ['influxdb'],
        components: {},
        watch: {},
        events: {
            'new-data': function (type, mydata) {
                // New data comes in ... from parent compoenent ...
                console.error("NEW DATA TYPE: %s .... %s", type, util.inspect(data, {depth: 10}))
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
                if (this.influxdb == null || this.influxdb == undefined) {
                    console.error("Nothing to Do ...")
                } else {
                    this.influxdb.query("show databases", function (err, results) {
                        console.error("ERROR: ", err)
                        console.error("RESULT: ", util.inspect(results, {depth: 10}))
                    })
                }
            }
        },
        computed: {}
    }

</script>