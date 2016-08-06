<style scoped>
</style>

<template>

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

            // Put some fake data; render it as heatmap ..
        },
        methods: {},
        computed: {}
    }

</script>