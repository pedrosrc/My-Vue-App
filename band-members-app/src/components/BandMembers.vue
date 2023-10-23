<script setup lang="ts">

import { reactive } from 'vue';

interface MembersProps {
  id: number,
  fname: string,
  lname: string,
  instrument: string
}

const members = reactive<MembersProps[]>([
  {
    id: 1,
    fname: 'John',
    lname: 'Lennon',
    instrument: 'Acoustic Guitar'
  },
  {
    id: 2,
    fname: 'George',
    lname: 'Harrison',
    instrument: 'Electric Guitar'
  }
])

let newMember = reactive({
  id: Number(Date.now() + Math.random() * 30),
  fname: '',
  lname: '',
  instrument: ''
})

function addMember() {
  if (newMember.fname && newMember.lname && newMember.instrument) {
    members.push(newMember);
    newMember = reactive({
      id: Number(Date.now()),
      fname: '',
      lname: '',
      instrument: ''
    })
  }else{
    return alert("Fields must be filled. Try Again!");
  }
  
}

</script>

<template>
  <section class="container">
    <h1>
      Band Members
    </h1>

    <table>
      <thead>
        <tr>
          <th>First Name</th>
          <th>Last Name</th>
          <th>Instrument</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="member in members" :key="member.id">
          <td>{{ member.fname }}</td>
          <td>{{ member.lname }}</td>
          <td>{{ member.instrument }}</td>
        </tr>
      </tbody>
    </table>

    <section class="add-more">
      <p>Add more band members</p>
      <form>
        <label for="fname">First name:</label><br>
        <input type="text" id="fname" name="fname" v-model="newMember.fname"><br>

        <label for="lname">Last name:</label><br>
        <input type="text" id="lname" name="lname" v-model="newMember.lname"><br>

        <label for="instrument">Instrument:</label><br>
        <select name="instrument" id="instrument" v-model="newMember.instrument">
          <option value="Bass">Bass</option>
          <option value="Electric Guitar">Electric Guitar</option>
          <option value="Acoustic Guitar">Acoustic Guitar</option>
          <option value="Drums">Drums</option>
        </select>
        <br><br>
        <input type="button" value="Add" @click="addMember()">
      </form>
    </section>
  </section>
</template>

<style scoped>

@import url('https://fonts.googleapis.com/css2?family=Metal+Mania&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Inter&family=Metal+Mania&display=swap');

.container {
  text-align: center;
  padding: 45px;
  font-family: 'Inter', Arial, Helvetica, sans-serif;
}
.container h1{
  font-family: 'Metal Mania';
}

.container table {
  margin: auto;
  font-size: 14px;
}

.container td,
.container th {
  padding: 8px;
  border-collapse: collapse;
}

.container th {
  border-bottom: 1px solid lightgrey;
}

.container p {
  margin-top: 0px;
}

.container form input,
.container form select {
  height: 24px;
  width: 240px;
  box-sizing: border-box;
}

.container form label {
  font-size: 12px;
}

section.add-more {
  box-shadow: rgba(0, 0, 0, 0.24) 0px 3px 8px;
  background-color: rgb(241, 241, 241);
  padding: 40px;
  margin-top: 40px;
}
</style>
