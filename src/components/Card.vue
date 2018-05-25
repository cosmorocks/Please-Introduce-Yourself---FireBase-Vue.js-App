<!-- In an effort to not repeat ourselves with the card structure in App.vue ... making Card into a Vue component. -->

<template>
    <div class="card">
        <div class="card-block">
            <h5 class="card-title"> {{ message.title }} </h5>
            <p class="card-text"> {{ message.text }} </p>
            <p class="card-text two"><small class="text-muted">{{ 'Added on ' + dateToString(message.timestamp) }} </small></p>
        </div>
    </div>
</template>
<script>
    import { dateToString } from '../utils/utils'
    export default {
        props:  ['message'], 
        methods: {
            dateToString
        }
    }
</script>

<style scoped>
    .card-block{
        text-align: left;
    }
    .card-title{
        padding: 10px;
    }
    .card-text{
        padding: 0 0 0px 10px;
    }
    .two{
        padding-bottom: 10px;
    }
</style>