<template>
  <div>
    <vue-good-table
      :columns="columns"
      :rows="rows"
      max-height="100px"
      :fixed-header="true"
      :sort-options="{
        enabled: false,
      }"
    />
  </div>
</template>

<script>
import "vue-good-table/dist/vue-good-table.css";
import { VueGoodTable } from "vue-good-table";
export default {
  name: "my-component",
  components: {
    VueGoodTable,
  },
  data() {
    return {
      columns: [
        {
          label: "Name",
          field: "name",
        },
        {
          label: "Age",
          field: "age",
          type: "number",
        },
      ],
      rows: [
        { id: 1, name: "John", age: 20 },
        {
          id: 2,
          name: "Jane",
          age: 24,
        },
        {
          id: 3,
          name: "Susan",
          age: 16,
        },
      ],
    };
  },
};
</script>
