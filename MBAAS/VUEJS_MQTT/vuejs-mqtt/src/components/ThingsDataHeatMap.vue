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
            'new-data': function (data) {
                // New data comes in ... from parent compoenent ...
                console.error("NEW DATA INCOMING ....", util.inspect(data, {depth: 10}))
            }
        },
        data () {
            return {}
        },
        ready () {

        },
        methods: {},
        computed: {}
    }

</script>