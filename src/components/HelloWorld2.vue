<template>
  <div class="vgt-wrap">
    <div class="vgt-inner-wrap">
      <div class="vgt-fixed-header">
        <table id="vgt-table" class="vgt-table bordered">
          <thead ref="fixedHeader">
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
      <div class="vgt-responsive" style="max-height: 150px">
        <table id="vgt-table" class="vgt-table bordered">
          <thead ref="originalHeader">
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
            <tr class="">
              <td class="vgt-left-align"><span> John </span></td>
              <td class="vgt-right-align"><span> 20 </span></td>
            </tr>
            <tr class="">
              <td class="vgt-left-align"><span> Jane </span></td>
              <td class="vgt-right-align"><span> 24 </span></td>
            </tr>
            <tr class="">
              <td class="vgt-left-align"><span> Susan </span></td>
              <td class="vgt-right-align"><span> 16 </span></td>
            </tr>
          </tbody>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "my-component2",
  data() {
    return {
      fixedColumns: [],
      originalColumns: [],
      ro: null,
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
  overflow-x: auto;
}

table.vgt-table {
  font-size: 16px;
  border-collapse: collapse;
  background-color: #fff;
  width: 100%;
  max-width: 100%;
  table-layout: auto;
  border: 1px solid #dcdfe6;
}

table {
  display: table;
  border-collapse: separate;
  box-sizing: border-box;
  text-indent: initial;
  border-spacing: 2px;
  border-color: grey;
}

thead {
  display: table-header-group;
  vertical-align: middle;
  border-color: inherit;
}

.vgt-table th {
  padding: 0.75em 1.5em 0.75em 0.75em;
  vertical-align: middle;
  position: relative;
}

.vgt-responsive {
  width: 100%;
  overflow-x: auto;
  position: relative;
}

table.vgt-table td {
  padding: 0.75em 0.75em 0.75em 0.75em;
  vertical-align: top;
  border-bottom: 1px solid #dcdfe6;
  color: #606266;
}
</style>
>
