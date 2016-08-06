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
</style>

<template>
    <div id="app">
        <h2>{{ msg }}</h2>

        <navigation></navigation>

        <div class="container">

            <div class="row">
            </div>

            <hr>

            <footer>Ninja Sensors 2016</footer>
        </div>

    </div>

</template>

<script>
    import Navigation from './components/Navigation.vue'

    export default {
        components: {
            navigation: Navigation
        },
        data () {
            return {
                // note: changing this line won't causes changes
                // with hot-reload because the reloaded component
                // preserves its current state and we are modifying
                // its initial state.
                msg: 'TheThingsNetwork Store with Ninja Detector'
            }
        }
    }
</script>

