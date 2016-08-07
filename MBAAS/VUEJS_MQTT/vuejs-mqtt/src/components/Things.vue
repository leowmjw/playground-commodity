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
                <h4>PIR</h4>
                <h2>{{ data.pir }}</h2>
            </div>
            <div>
                <h4>DOOR</h4>
                <h2>{{ data.door }}</h2>
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
                // console.error("NEW DATA TYPE: %s .... %s", type, util.inspect(mydata.fields, {depth: 10}))
                // this.raw = mydata
                if (mydata.fields == null || mydata.fields == undefined) {
                    console.error("FIELDS EMPTY ..")

                } else {
                    switch (this.slot) {
                        case "1":
                            this.data.pir += mydata.fields.pirValue1
                            this.data.door += mydata.fields.magValue1
                            break
                        case "2":
                            this.data.pir += mydata.fields.pirValue2
                            this.data.door += mydata.fields.magValue2
                            break
                        case "3":
                            this.data.pir += mydata.fields.pirValue3
                            this.data.door += mydata.fields.magValue3
                            break
                        case "4":
                            this.data.pir += mydata.fields.pirValue4
                            this.data.door += mydata.fields.magValue4
                            break
                        case "5":
                            this.data.pir += mydata.fields.pirValue5
                            this.data.door += mydata.fields.magValue5
                            break
                        case "6":
                            this.data.pir += mydata.fields.pirValue6
                            this.data.door += mydata.fields.magValue6
                            break
                        case "7":
                            this.data.pir += mydata.fields.pirValue7
                            this.data.door += mydata.fields.magValue7
                            break
                        case "8":
                            this.data.pir += mydata.fields.pirValue8
                            this.data.door += mydata.fields.magValue8
                            break
                        case "9":
                            this.data.pir += mydata.fields.pirValue9
                            this.data.door += mydata.fields.magValue9
                            break
                        case "10":
                            this.data.pir += mydata.fields.pirValue10
                            this.data.door += mydata.fields.magValue10
                            break
                        default:
                            break
                    }
                }
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