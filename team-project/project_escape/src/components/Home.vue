<template>
    <div class="container">
        <Todo></Todo>
        <stopwatch></stopwatch>
        <Clock></Clock>
    </div>
</template>

<script>
import Todo from '../components/page3/todo2.vue';
import stopwatch from '../components/page3/stopwatch.vue';
import Clock from "../components/page3/Clock.vue";


export default {
    components: {
    'Todo' : Todo,
    'stopwatch' : stopwatch,
    'Clock':Clock,
    },
};
</script>