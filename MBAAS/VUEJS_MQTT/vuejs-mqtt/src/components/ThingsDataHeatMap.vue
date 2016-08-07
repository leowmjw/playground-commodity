<style scoped>
    .demo-wrapper {
        height: 500px;
        background: rgba(0, 0, 0, .03);
        border: 3px solid black;
    }

    .heatmap {
        width: 100%;
        height: 100%;
    }

</style>

<template>

    <div class="col-md-12  demo-wrapper">
        <h2>Foot Traffic HeatMap</h2>
        <div class="heatmap">
            <canvas class="heatmap-canvas">
            </canvas>
        </div>
    </div>

</template>

<script>

    import util from 'util'
    // Actual subcomponents neede below ..

    // Actual libs needed below ...

    export default {
        props: [],
        components: {},
        watch: {},
        events: {
            'new-data': function (type, mydata) {
                // New data comes in ... from parent compoenent ...
                //console.error("NEW DATA INCOMING ....", util.inspect(mydata, {depth: 10}))
                // Fill in the latest data

                if (mydata.fields == null || mydata.fields == undefined) {

                } else {
                    console.error("UPDATE_HEAT_MAP!!!!")
                    for (let item of this.nodes) {
                        switch (item.label) {
                            case "node1":
                                this.accumulated_data.node1.pir += Number.parseInt(mydata.fields.pirValue1)
                                this.accumulated_data.node1.door += Number.parseInt(mydata.fields.magValue1)
                                break
                            case "node2":
                                this.accumulated_data.node2.pir += Number.parseInt(mydata.fields.pirValue2)
                                this.accumulated_data.node2.door += Number.parseInt(mydata.fields.magValue2)
                                break
                            case "node3":
                                this.accumulated_data.node3.pir += Number.parseInt(mydata.fields.pirValue3)
                                this.accumulated_data.node3.door += Number.parseInt(mydata.fields.magValue3)
                                break
                            case "node4":
                                this.accumulated_data.node4.pir += Number.parseInt(mydata.fields.pirValue4)
                                this.accumulated_data.node4.door += Number.parseInt(mydata.fields.magValue4)
                                break
                            case "node5":
                                this.accumulated_data.node5.pir += Number.parseInt(mydata.fields.pirValue5)
                                this.accumulated_data.node5.door += Number.parseInt(mydata.fields.magValue5)
                                break
                            case "node6":
                                this.accumulated_data.node6.pir += Number.parseInt(mydata.fields.pirValue6)
                                this.accumulated_data.node6.door += Number.parseInt(mydata.fields.magValue6)
                                break
                            case "node7":
                                this.accumulated_data.node7.pir += Number.parseInt(mydata.fields.pirValue7)
                                this.accumulated_data.node7.door += Number.parseInt(mydata.fields.magValue7)
                                break
                            case "node8":
                                this.accumulated_data.node8.pir += Number.parseInt(mydata.fields.pirValue8)
                                this.accumulated_data.node8.door += Number.parseInt(mydata.fields.magValue8)
                                break
                            case "node9":
                                this.accumulated_data.node9.pir += Number.parseInt(mydata.fields.pirValue9)
                                this.accumulated_data.node9.door += Number.parseInt(mydata.fields.magValue9)
                                break
                            default:
                                break
                        }
                    }
                    // Increase the accumulated data
                    console.error("UPDATED_ACCUMULATED: ", util.inspect(this.accumulated_data, {depth: 10}))
                    this.refreshData()
                }
            }
        },
        data () {
            return {
                nodes: [{
                    label: "node1",
                    pos: {x: 270, y: 140}
                }, {
                    label: "node2",
                    pos: {x: 400, y: 325}
                }, {
                    label: "node3",
                    pos: {x: 450, y: 200}
                }, {
                    label: "node4",
                    pos: {x: 600, y: 250}
                }, {
                    label: "node5",
                    pos: {x: 700, y: 250}
                }, {
                    label: "node6",
                    pos: {x: 150, y: 150}
                }, {
                    label: "node7",
                    pos: {x: 170, y: 70}
                }, {
                    label: "node8",
                    pos: {x: 100, y: 50}
                }],
                accumulated_data: {
                    node1: {pir: 0, door: 0},
                    node2: {pir: 0, door: 0},
                    node3: {pir: 0, door: 0},
                    node4: {pir: 0, door: 0},
                    node5: {pir: 0, door: 0},
                    node6: {pir: 0, door: 0},
                    node7: {pir: 0, door: 0},
                    node8: {pir: 0, door: 0}
                },
                heatmap_canvas: null
            }
        },
        ready () {
            // this.simulateHeatMap()
            this.initHeatMap()
        },
        methods: {
            simulateHeatMap: function () {
                // minimal heatmap instance configuration
                var heatmapInstance = h337.create({
                    // only container is required, the rest will be defaults
                    container: document.querySelector('.heatmap')
                });

                // now generate some random data
                var points = [];
                var max = 0;
                var width = 800;
                var height = 350;
                var len = 300;

                while (len--) {
                    var val = Math.floor(Math.random() * 100);
                    // now also with custom radius
                    var radius = Math.floor(Math.random() * 70);

                    max = Math.max(max, val);
                    var point = {
                        x: Math.floor(Math.random() * width),
                        y: Math.floor(Math.random() * height),
                        value: val,
                        // radius configuration on point basis
                        radius: radius
                    };
                    points.push(point);
                }
                // heatmap data format
                var data = {
                    max: max,
                    data: points
                };
                // if you have a set of datapoints always use setData instead of addData
                // for data initialization
                heatmapInstance.setData(data);
            },
            initHeatMap: function () {
                // Have 8 nodes for demo??
                const heatmapInstance = h337.create({
                    // only container is required, the rest will be defaults
                    container: document.querySelector('.heatmap')
                })

                // Set the handler
                this.heatmap_canvas = heatmapInstance
                // randomize data ..
                // this.randomData()
                this.refreshData()
            },
            randomData: function () {
                // Canvas size; how to adjust dynamically??

                const width = 800
                const height = 350

                let points = []
                let max = 0

                // Loop through each location; get accumulated as value
                for (let item of this.nodes) {
                    // console.error("ITEM: ", util.inspect(item, {depth: 10}))
                    // console.error("ACC_VAL: PIR: %s DOOR: %s", this.accumulated_data.node1.pir, this.accumulated_data.node1.door)
                    let value = 1 + Math.floor(Math.random() * 10)
                    // What shoule be the radius??
                    let radius = Math.floor(value * 7)

                    max = Math.max(max, value)

                    points.push({
                        x: item.pos.x,
                        y: item.pos.y,
                        value: value,
                        radius: radius
                    })

                    let mydata = {
                        max: max,
                        data: points
                    }

                    // console.error("PLOT: ", util.inspect(mydata, {depth: 10}))
                    this.heatmap_canvas.setData(mydata)
                }
            },
            refreshData: function () {
                // Canvas size; how to adjust dynamically??

                const width = 800
                const height = 350

                let points = []
                let max = 0

                // Loop through each location; get accumulated as value
                for (let item of this.nodes) {
                    // console.error("ITEM: ", util.inspect(item, {depth: 10}))
                    // console.error("ACC_VAL: PIR: %s DOOR: %s", this.accumulated_data.node1.pir, this.accumulated_data.node1.door)
                    let accumulated_value = 0
                    switch(item.label) {
                        case "node1":
                            accumulated_value = this.accumulated_data.node1.pir + this.accumulated_data.node1.door
                            break
                        case "node2":
                            accumulated_value = this.accumulated_data.node2.pir + this.accumulated_data.node2.door
                            break
                        case "node3":
                            accumulated_value = this.accumulated_data.node3.pir + this.accumulated_data.node3.door
                            break
                        case "node4":
                            accumulated_value = this.accumulated_data.node4.pir + this.accumulated_data.node4.door
                            break
                        case "node5":
                            accumulated_value = this.accumulated_data.node5.pir + this.accumulated_data.node5.door
                            break
                        case "node6":
                            accumulated_value = this.accumulated_data.node6.pir + this.accumulated_data.node6.door
                            break
                        case "node7":
                            accumulated_value = this.accumulated_data.node7.pir + this.accumulated_data.node7.door
                            break
                        case "node8":
                            accumulated_value = this.accumulated_data.node8.pir + this.accumulated_data.node8.door
                            break
                        case "node9":
                            accumulated_value = this.accumulated_data.node9.pir + this.accumulated_data.node9.door
                            break
                        default:
                            break
                    }
                    let value = Math.floor(accumulated_value)
                    // What shoule be the radius??
                    let radius = Math.floor(value * 5)

                    max = Math.max(max, value)

                    points.push({
                        x: item.pos.x,
                        y: item.pos.y,
                        value: value,
                        radius: radius
                    })

                    let mydata = {
                        max: max,
                        data: points
                    }

                    // console.error("PLOT: ", util.inspect(mydata, {depth: 10}))
                    this.heatmap_canvas.setData(mydata)
                }
            }
        },
        computed: {}
    }

</script>