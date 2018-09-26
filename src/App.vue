<template>
    <div id="app">
        <Calendar />
    </div>
</template>

<script>
    import HelloWorld from './components/HelloWorld'
    import Calendar from './components/Calendar'
    // import Slide from './components/Slide'

    export default {
        name: 'App',
        components: {Calendar},
    }
</script>

<style scoped lang="scss">
    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin: 50px 0 0;
    }



</style>
