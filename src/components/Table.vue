<template>
  <div class="table">
  <div>
    <table style="width: 75%; text-align: center;" border="2" cellpadding="1">
      <tbody>
        <tr>
          <td>Nazwa produktu</td>
          <td>Cena</td>
          <td>Ilość sztuk</td>
        </tr>
        <tr v-for="tables in tableName" :key="tables.id">
          <td>{{tables.title}}</td>
          <td>{{tables.price}}</td>
          <td>{{tables.count}}</td>
        </tr>
      </tbody>
    </table>
  </div>
  </div>
</template>

<script>
export default {
  name: "table",
  props: ["tableName"]
};
</script>

<style>
td {
  padding: 35px;
}
</style>
