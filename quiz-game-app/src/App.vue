<script setup lang="ts">


// https://opentdb.com/api.php?amount=10

// const questions = []


</script>

<template>

  <header>
      <h1>Quiz Game</h1>
  </header>
  
  <main>
    <section class="question">
      <h1>Hello World!</h1>
    </section>

    <section class="items">
      <input type="radio" name="options" value="true">
      <label>True</label><br>

      <input type="radio" name="options" value="false">
      <label>False</label><br>

      <button class="send" type="button">Send</button>
    </section>

  </main>

</template>

<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Inter&family=Josefin+Sans&family=Metal+Mania&family=Russo+One&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter&family=Josefin+Sans&family=Metal+Mania&display=swap');

header{
  display: flex;
  justify-content: center;
  margin: 30px;
  margin-top: 50px;
  font-family: 'Russo One', Arial, Helvetica, sans-serif;
}

header h1{
  background-color: blue;
  padding: 10px;
  border-radius: 20px;
  color: #00a8e8;
  font-size: 3rem;
  box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
}

main{
  margin: auto;
  margin-top: 50px;
  min-width: 300px;
  max-width: 1000px;
  padding: 20px;
  font-family: 'Josefin Sans', Arial, Helvetica, sans-serif;
}
.question{
  text-align: center;
  font-size: 1.8rem;
}
.items{
  margin: 20px;
  font-size: 1.2rem;
  text-align: center;
}
.items input{
  cursor: pointer;
}

.send{
  margin: 10px auto;
  font-family: 'Josefin Sans', Arial, Helvetica, sans-serif;
  cursor: pointer;
  border-radius: 10px;
  border: none;
  background-color: blue;
  color: #fff;
  text-align: center;
  padding: 5px;
  width: 150px;
  font-size: 1.5rem;
}
.send:hover{
  transition: .3s;
  background-color: #00a8e8;
  border-radius: 20px;
}

</style>
