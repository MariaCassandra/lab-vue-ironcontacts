<template>
  <div>
    <h1>Iron Contacts</h1>
    <div class="sortingButtons">
    <button @click="getRandomElem">Add a Random Contact</button>
    <button @click="mostPopular">Sort by popularity</button>
    <button @click="alphabetic">Sort by name</button>
    </div>
    <table class="table">
      <thead class="conceptLine">
        <td><b>Picture</b></td>
        <td><b>Name</b></td>
        <td><b>Popularity</b></td>
        <td><b>Won an Oscar</b></td>
        <td><b>Won an Emmy</b></td>
        <td><b>Actions</b></td>
      </thead>
      <tbody>
        <tr v-for="contact in fiveContacts" :key="contact.id">
          <td><img :src="`${ contact.pictureUrl }`" class="actor-img"/></td>
          <td> {{ contact.name }} </td>
          <td> {{ contact.popularity }} </td>
          <td>{{ contact.wonOscar ? "🏆" : "" }}</td>
          <td>{{ contact.wonEmmy ? "🏆" : "" }}</td>
          <td><button @click="deleteElem(contact.id)">Delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import contactsData from "./contacts.json";
export default {
  name: 'App',
  data() {
    return {
      contacts: contactsData,
      fiveContacts: [],
    }
  },
  created() {
    for (let i = 0; i < 5; i++) {
      this.fiveContacts.push(this.contacts.shift())
    }
  },
  methods: {
    getRandomInt(min, max) {
      min = Math.ceil(min);
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - min) + min);
    },
    getRandomElem() {
      if (this.contacts.length) {
        const randomPos = this.getRandomInt(0, this.contacts.length - 1);
        const randomElem = this.contacts[randomPos];
        const elemToShow = this.fiveContacts.findIndex(elem => elem === randomElem);
        if (elemToShow === -1) {
          this.fiveContacts.push(randomElem);
          const elemToRemoveIndex = this.contacts.findIndex(elem => elem === randomElem);
          this.contacts.splice(elemToRemoveIndex, 1);
        }
      }
    },
    mostPopular() {
      this.fiveContacts.sort((a,b) => a.popularity < b.popularity ? 1 : -1);
    },
    alphabetic() {
      this.fiveContacts.sort((a,b) => a.name > b.name ? 1 : -1);
    },
    deleteElem(contactId) {
      const contactToDelete = this.fiveContacts.findIndex(elem => elem.id === contactId);
      if (contactToDelete !== -1) {
        this.contacts.push(this.fiveContacts.splice(contactToDelete, 1)[0]);
      }
    }
  },
};
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
  justify-content: space-between;
  align-items: center;
  gap: 20px;
  margin-bottom: 20px;
}
.table > thead > td {
  padding-left: 60px;
}
.table > tbody > tr > td {
  padding-left: 30px;
}
button {
  background-color: #3498db;
  color: #fff;
  border: none;
  padding: 10px;
  border-radius: 5px;
  cursor: pointer;
}
</style>
