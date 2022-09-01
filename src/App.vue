<template>
  <div id="app">
  <h1>IronContacts</h1>
  <table>
    <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
        </tr>
    </thead>
    <tbody>
        <tr v-for="contact in firstFiveContacts" :key="contact.id">
          <td><img :src="contact.pictureUrl"></td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
        </tr>
    </tbody>
  </table>
  </div>
</template>

<script setup>
import contacts from './contacts.json'
import { ref, reactive } from 'vue'

const myContacts = reactive(contacts);
const firstFiveContacts = reactive(myContacts.slice(0, 5));
const otherContacts = reactive(firstFiveContacts.slice(5));
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

img {
  width: 100px;
}
</style>
