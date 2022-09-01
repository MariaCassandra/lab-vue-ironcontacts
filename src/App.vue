<template>
  <div id="app">
    <h1>IronContacts</h1>
    <div class="sortingButtons">
      <button @click="addRandomActor">Add Random Contact</button>
      <button @click="sortByPopularity">Sort by popularity</button>
      <button @click="sortByName">Sort by name</button>
    </div>
    <table>
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won an Oscar</th>
          <th>Won an Emmy</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in firstFiveContacts" :key="contact.id">
          <td><img :src="contact.pictureUrl" /></td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td>{{ contact.wonOscar ? "🏆" : "" }}</td>
          <td>{{ contact.wonEmmy ? "🏆" : "" }}</td>
          <td><button @click="deleteContact">Delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import contacts from "./contacts.json";
import { reactive } from "vue";

const myContacts = reactive(contacts);
const firstFiveContacts = reactive(myContacts.slice(0, 5));
const otherContacts = reactive(firstFiveContacts.slice(5));

function addRandomActor() {
  const randomNumber = Math.floor(Math.random() * this.otherContacts.length);
  this.firstFiveContacts.push(otherContacts[randomNumber]);
  this.otherContacts.splice(randomNumber, 1);
}

function sortByPopularity() {
  this.firstFiveContacts.sort((a, b) => (a.popularity < b.popularity ? 1 : -1));
}

function sortByName() {
  this.firstFiveContacts.sort((a, b) => (a.name > b.name ? 1 : -1));
}

function deleteContact(contact) {
  const index = firstFiveContacts.indexOf(contact);
  firstFiveContacts.splice(index, 1);
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  text-align: center;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 20px;
}

img {
  width: 100px;
}

.sortingButtons {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: center;
  gap: 20px;
}
</style>
