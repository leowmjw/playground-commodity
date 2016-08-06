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
                console.error("NEW DATA INCOMING ....", util.inspect(mydata, {depth: 10}))
                // Fill in the latest data

                // Increase the accumulated data
            }
        },
        data () {
            return {
                latest_data: null,
                accumulated_data: null
            }
        },
        ready () {
            this.simulateHeatMap()
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

                // Canvas size; how to adjust dynamically??

                const width = 600
                const height = 300

                const nodes = [{
                    label: "Node1",
                    pos: {x: 10, y: 10}
                }, {
                    label: "Node2",
                    pos: {x: 100, y: 25}
                }, {
                    label: "Node3",
                    pos: {x: 30, y: 200}
                }, {
                    label: "Node4",
                    pos: {x: 300, y: 250}
                }]

                let points = []
                let max = 0

                // Loop through each location; get accumulated as value
                for (let item of nodes) {
                    console.error("ITEM: ", util.inspect(item, {depth: 10}))
                }
                let value = 1
                // What shoule be the radius??
                let radius = Math.floor(value * 0.7)

                max = Math.max(max, value)

                points.push({
                    x: 100,
                    y: 111,
                    value: value,
                    radius: radius
                })

                let mydata = {
                    max: max,
                    data: points
                }

                // heatmapInstance.setData(mydata)
            }
        },
        computed: {}
    }

</script>