<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <p>
      <label for="categories">Choose a category: </label>
      <select v-model="selectedCategory" id="categories" name="categories">
        <option value="All">All</option>
        <option value="Book">Books</option>
        <option value="Magazine">Magazines</option>
        <option value="Newspaper">Newspapers</option>
        <option value="Other">Others</option>
      </select>
    </p>
    <p>
      <label for="item">Search an Item: </label>
      <input
        type="text"
        v-model="searchText"
        placeholder="Name or description"
        id="item"
        name="item"
      />
    </p>
    <table id="t01">
      <thead>
        <tr>
          <th>Code</th>
          <th>Name</th>
          <th>Description</th>
          <th>Category</th>
        </tr>
      </thead>
      <tbody :key="itemsDBElem.code" v-for="itemsDBElem in filteredList">
        <tr>
          <td>{{ itemsDBElem.code }}</td>
          <td>{{ itemsDBElem.name }}</td>
          <td>{{ itemsDBElem.description }}</td>
          <td>{{ itemsDBElem.category }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: "HelloWorld",
  data() {
    return {
      selectedCategory: "All",
      searchText: ""
    };
  },
  props: {
    msg: String,
    itemsDB: {
      type: Array,
      default: function() {
        return [];
      }
    }
  },
  computed: {
    filteredList() {
      const filteredCategoryList =
        this.selectedCategory === "All"
          ? this.itemsDB
          : this.itemsDB.filter(
              itemsDBElem => itemsDBElem.category === this.selectedCategory
            );
      return this.searchText == ""
        ? filteredCategoryList
        : filteredCategoryList.filter(
            itemsDBElem =>
              itemsDBElem.name
                .toLowerCase()
                .includes(this.searchText.toLowerCase()) ||
              itemsDBElem.description
                .toLowerCase()
                .includes(this.searchText.toLowerCase())
          );
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
table {
  margin-left: auto;
  margin-right: auto;
  width: 80%;
}
table,
th,
td {
  border: 2px solid black;
  border-collapse: collapse;
  padding: 15px;
}
th {
  text-align: center;
  background-color: #3a4750;
  color: #eeeeee;
}
td {
  text-align: left;
}
td:nth-child(even) {
  background-color: #eee;
}
td:nth-child(odd) {
  background-color: #fff;
}
label {
  font-size: 1.5em;
}
</style>
