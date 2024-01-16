<template>
  <h1 class="title">Nova polozka</h1>
  <div class="form">
    <label for="text-input">Nazov polozky:</label>
    <input class="input" id="text-input" v-model="input" />
    <button class="add-button" @click="addItem()">Add to list</button>
  </div>

  <hr />

  <h2>Polozky</h2>
  <ul class="valid-items">
    <li v-for="item in validItems" :key="`item-${item.id}`">
      <span class="delete-button" @click="deleteItem(item)">X</span>
      <span>{{ item.text }}</span>
    </li>
  </ul>

  <hr />

  <h2>Zmazane polozky</h2>
  <ul class="deleted-items">
    <li v-for="item in deletedItems" :key="`item-${item.id}`">
      <span>{{ item.text }}</span>
    </li>
  </ul>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      input: "",
      items: [
        { id: 1, text: "Item 1", is_deleted: false },
        { id: 2, text: "Item 2", is_deleted: false },
        { id: 3, text: "Item 3", is_deleted: false },
      ],
    };
  },
  methods: {
    addItem() {
      if (this.input == "") {
        alert("Zadajte nazov!");
        return;
      }
      this.items.push({
        id: this.items.length + 1,
        text: this.input,
        is_deleted: false,
      });
      this.input = "";
    },
    deleteItem(item) {
      item.is_deleted = true;
    },
  },
  computed: {
    validItems() {
      return this.items.filter((item) => !item.is_deleted);
    },
    deletedItems() {
      return this.items.filter((item) => item.is_deleted);
    },
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
  margin-top: 60px;
}

.title {
  color: var(--primary-color);
  font-weight: bold;
}

.form {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  align-content: center;
  margin: auto;
  width: 20rem;
}

.form label {
  margin: 0;
  text-align: start;
  font-weight: bold;
}

.input {
  height: 2rem;
  border-radius: 7px;
  border: 2px solid var(--primary-color);
  font-size: 1.2rem;
}

.input:focus {
  border-color: 3px solid var(--primary-color);
}

.add-button {
  background-color: var(--primary-color);
  color: #fff;
  padding: 0.5rem;
  font-size: 1.2rem;
  border: none;
  border-radius: 7px;
  margin-bottom: 1rem;
  transition: all 300ms ease-in-out;
}

.add-button:hover {
  opacity: 0.8;
  transition: all 300ms ease-in-out;
  cursor: pointer;
}

.valid-items,
.deleted-items {
  list-style-type: none;
  padding: 0;
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
}

.valid-items,
.deleted-items li {
  color: var(--primary-color);
  font-size: 1.2rem;
}

.delete-button {
  margin-right: 15px;
  color: red;
  transition: all 300ms ease-in-out;
}

.delete-button:hover {
  cursor: pointer;
  font-weight: bold;
  transition: all 400ms ease-in-out;
}

.deleted-items li {
  text-decoration: line-through;
}
</style>
