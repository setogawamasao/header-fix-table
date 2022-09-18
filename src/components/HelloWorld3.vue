<template>
  <div class="vgt-wrap">
    <div class="vgt-fixed-header">
      <table class="table is-striped vgt-table">
        <thead>
          <tr>
            <th
              v-for="(column, index) in columns"
              :key="index"
              :ref="setFixedColumn"
            >
              {{ column.label }}
            </th>
          </tr>
        </thead>
      </table>
    </div>
    <div class="vgt-responsive" style="max-height: 160px">
      <table class="table is-striped vgt-table">
        <thead>
          <tr>
            <th
              v-for="(column, index) in columns"
              :key="index"
              :ref="setOriginalColumn"
            >
              {{ column.label }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="(row, index) in rows" :key="index">
            <td>{{ row.name }}</td>
            <td>{{ row.age }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import "bulma/css/bulma.css";
export default {
  name: "my-component2",
  data() {
    return {
      columns: [{ label: "Name" }, { label: "Age" }],
      rows: [
        { id: 1, name: "John", age: 20 },
        { id: 2, name: "Jane", age: 24 },
        { id: 3, name: "Susan", age: 16 },
        { id: 4, name: "mike", age: 20 },
      ],
      fixedColumns: [],
      originalColumns: [],
    };
  },
  mounted() {
    window.addEventListener("resize", this.resize);
  },
  updated() {
    this.resize();
  },
  methods: {
    setFixedColumn(el) {
      if (el) {
        this.fixedColumns.push(el);
      }
    },
    setOriginalColumn(el) {
      if (el) {
        this.originalColumns.push(el);
      }
    },
    resize() {
      console.log("resize2");
      this.fixedColumns.forEach((fixedColumn, index) => {
        const originalColumnWidth = window.getComputedStyle(
          this.originalColumns[index],
          null
        ).width;
        fixedColumn.setAttribute("width", originalColumnWidth);
      });
    },
  },
};
</script>

<style scoped>
.vgt-wrap {
  position: relative;
}

.vgt-fixed-header {
  position: absolute;
  z-index: 10;
  background-color: #fff;
}

.vgt-responsive {
  overflow-y: scroll;
}

.vgt-table {
  width: 100%;
  /* border: 1px solid #000000;
  border-collapse: collapse; */
}

/* .vgt-table th {
  border: 1px solid #000000;
}

.vgt-table td {
  border: 1px solid #000000;
} */
</style>
