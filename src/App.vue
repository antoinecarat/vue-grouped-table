<template>
  <div id="app">
    <h1>Grouped Table Demo</h1>
    <div class="groupby-form">
      <label for="groupby">Group by: </label>
      <select name="groupby" v-model="current">
        <option
          v-for="prop in properties.filter(e => !selectedProps.includes(e))"
          :key="prop"
          >{{ prop }}</option
        >
      </select>
      <button @click="selectProp()">+</button>
      <span
        class="prop"
        v-for="(prop, i) in selectedProps"
        :key="prop"
        @click="selectedProps.splice(i, 1)"
        >{{ prop }}
      </span>
    </div>
    <GroupedTable :headers="selectedProps" :entries="entries" />
  </div>
</template>

<script>
import GroupedTable from "./components/GroupedTable.vue";

export default {
  name: "app",
  components: {
    GroupedTable
  },
  data: function() {
    return {
      properties: ["city", "name", "age", "genre"],
      selectedProps: [],
      current: "",
      entries: [
        { city: "Dublin", name: "Antoine", age: 23, genre: "M" },
        { city: "Dublin", name: "Margaux", age: 24, genre: "F" },
        { city: "Nantes", name: "Mattis", age: 23, genre: "M" },
        { city: "Nantes", name: "Hugo", age: 24, genre: "M" },
        { city: "Nantes", name: "Laurie", age: 23, genre: "F" },
        { city: "Marrakech", name: "Amr", age: 25, genre: "M" }
      ]
    };
  },
  methods: {
    selectProp() {
      if (this.current !== "") {
        this.selectedProps.push(this.current);
        this.current = "";
      }
    }
  }
};
</script>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;

  display: flex;
  flex-flow: column nowrap;
  justify-content: flex-start;
  align-items: flex-start;
  padding: 2%;
  width: 50%;
}

.groupby-form {
  align-self: flex-start;
  width: 100%;
  margin-bottom: 1rem;
  padding-bottom: 0.5rem;
  border-bottom: 1px dashed #2c3e50;

  .prop {
    margin: 0 0.2rem;
    cursor: pointer;

    &:hover {
      text-decoration: underline;
      color: lighten($color: #2c3e50, $amount: 30);
      &::after {
        content: " x";
        font-weight: 600;
        color: #2c3e50;
      }
    }
  }

  button {
    cursor: pointer;
    margin-right: 2rem;
  }
}
</style>
