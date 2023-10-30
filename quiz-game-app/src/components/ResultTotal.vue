<script setup lang="ts">
import { onMounted, reactive } from 'vue';

const props = defineProps(['resultTotal'])

let templateText = reactive({
    emoji: "undefined",
    title: "undefined",
    text: "undefined"
})

function ReloadPage() {
    location.reload();
}
onMounted(() => {
    if (props.resultTotal === true) {
        templateText.emoji = "&#127881;"
        templateText.title = "Winner !"
        templateText.text = "Congratulations, You Win!"
    } else {
        templateText.emoji = "&#128532;"
        templateText.title = "Game Over !"
        templateText.text = "It wasn't this time, Try Again!"
    }
});

</script>
<template>
    <section class="container_total">
        <div class="results">
            <span v-html="templateText.emoji"></span>
            <h1 v-html="templateText.title"></h1>
            <p v-html="templateText.text"></p>
            <button @click="ReloadPage">Try Again</button>
        </div>
    </section>
</template>

<style scoped>
.container_total{
    display: flex;
    position: absolute;
    width: 100vh;
    background-color: white;
}
.results{
    text-align: center;
    color: #fff;
    width: 800px;
    background-color: blue;
    font-size: 1.5em;
    padding: 20px;
    border-radius: 15px;
    margin: 0 auto;
}

.results button {
  margin: 20px auto;
  font-family: 'Josefin Sans', Arial, Helvetica, sans-serif;
  cursor: pointer;
  border-radius: 10px;
  border: none;
  background-color: #00a8e8;
  color: #fff;
  text-align: center;
  padding: 5px;
  width: 150px;
  font-size: 1.5rem;
}


</style>