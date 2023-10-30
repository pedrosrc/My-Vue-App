<script setup lang="ts">

const props = defineProps(['winCount', 'loseCount'])

</script>

<template>
    <section class="container_score">
        Player
        <span>{{ props.winCount }}</span>
        x
        <span>{{ props.loseCount }}</span>
        CPU
    </section>
</template>

<style scoped>
.container_score{
    background-color: blue;
    color: #fff;
    width: 50%;
    border-radius: 15px;
    text-align: center;
    font-size: 1.5em;
    border-bottom: 1px solid #000;
    padding: 20px;
    margin: 0 auto;
    margin-bottom: 30px;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
}
.container_score > span{
    border-radius: 50%;
    color: #000;
    background-color: #fff;
    border: 1px solid #000;
    font-weight: bold;
    padding: 5px;
}
</style>