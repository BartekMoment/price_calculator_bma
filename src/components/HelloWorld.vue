<template>
    <div class="hello">
      <label class="typo__label">Wybierz produkt:</label>
      <multiselect v-model="value" :options="options" :custom-label="nameWithLang" placeholder="Select one" label="name" track-by="id"></multiselect>
      <div class="count__numer">
        <button v-on:click="count++">+</button>
        {{ count + ' szt.' }}
        <button v-on:click="count--">-</button>
      </div>
      <input disabled type="text" id="result" v-model="resultAdds">
      <form v-on:submit.prevent="addNewTodo">
        <button>Dodaj +</button>
      </form>
      <Table :table-name="todos"/>
    <button><JsonExcel :fields="fields" :data="todos"/></button>
    </div>
</template>

<script>
import myjson from "../../static/date.json";
import JsonExcel from 'vue-json-excel'
import Table from './Table'

export default {
  name: "HelloWorld",
	components:{
    JsonExcel,
    Table
  },
  data() {
    return {
      fields: {
				'Nazwa produktu':'title',
        'Ilość sztuk': 'count',
				'Cana':'price'
			},
      value: { name: "Nazwa produktu", price: "Cena" },
      options: myjson,
      count: 1,
      todos: []
    };
  },
  methods: {
        filterItems: function(e){
          console.log(JSON.stringify(this.todos))
        },
    nameWithLang({ name, price }) {
      return `${name} — [${price}]`;
    },
    addNewTodo: function() {
      this.todos.push({
        title: this.value.name,
        price: this.value.price * this.count,
        count: this.count
      });
    }
  },
  computed: {
    resultAdds: function() {
      return this.value.price * this.count + " zł";
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  display: flex;
  flex-flow: column wrap;
  height: 100%;
}
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
