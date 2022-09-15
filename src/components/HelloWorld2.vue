<template>
  <div class="vgt-wrap">
    <div class="vgt-fixed-header">
      <table class="vgt-table">
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
    <div class="vgt-responsive" style="max-height: 80px">
      <table class="vgt-table">
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
  border: 1px solid #000000;
  border-collapse: collapse;
}

.vgt-table th {
  border: 1px solid #000000;
}

.vgt-table td {
  border: 1px solid #000000;
}
</style>
