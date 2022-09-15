<template>
  <div class="vgt-wrap">
    <div class="vgt-inner-wrap">
      <div class="vgt-fixed-header">
        <table id="vgt-table" class="vgt-table bordered">
          <colgroup>
            <col id="col-0" />
            <col id="col-1" />
          </colgroup>
          <thead ref="fixedHeader">
            <tr>
              <th
                v-for="(column, index) in columns"
                scope="col"
                :key="index"
                :ref="setFixedColumn"
              >
                {{ column.label }}
              </th>
              <!-- <th
                scope="col"
                aria-sort="descending"
                aria-controls="col-0"
                class="vgt-left-align"
                style="width: 723.727px"
              >
                <span>Name</span>
              </th>
              <th
                scope="col"
                aria-sort="descending"
                aria-controls="col-1"
                class="vgt-right-align"
                style="width: 598.289px"
              >
                <span>Age</span>
              </th>
            </tr> -->
            </tr>
          </thead>
        </table>
      </div>
      <div class="vgt-responsive" style="max-height: 100px">
        <table id="vgt-table" class="vgt-table bordered">
          <colgroup>
            <col id="col-0" />
            <col id="col-1" />
          </colgroup>
          <thead ref="originalHeader">
            <tr>
              <th
                v-for="(column, index) in columns"
                scope="col"
                style=""
                :key="index"
                :ref="setOriginalColumn"
              >
                {{ column.label }}
              </th>
              <!-- <th
                scope="col"
                aria-sort="descending"
                aria-controls="col-0"
                class="vgt-left-align"
                style="min-width: auto; width: auto"
              >
                <span>Name</span>
              </th>
              <th
                scope="col"
                aria-sort="descending"
                aria-controls="col-1"
                class="vgt-right-align"
                style="min-width: auto; width: auto"
              >
                <span>Age</span>
              </th> -->
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
      originalHeader: {},
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
        // const width = window.getComputedStyle(
        //   this.originalColumns[index],
        //   null
        // ).width;
        const width = window.getComputedStyle(
          this.$refs.originalHeader.rows[0].cells[index],
          null
        ).width;
        fixedColumn.setAttribute("width", width);
      });
    },
  },
  beforeUpdate() {
    this.resize();
    // this.fixedColumns = [];
    // this.originalColumns = [];
  },
  updated() {
    this.resize();
  },
  watch: {
    originalHeader: {
      handler() {
        this.resize();
      },
      immediate: true,
    },
  },
  mounted() {
    window.addEventListener("resize", this.resize);
  },
};
</script>

<style scoped>
.vgt-wrap {
  position: relative;
}

div {
  display: block;
}

.vgt-inner-wrap {
  border-radius: 0.25rem;
  -webkit-box-shadow: 0 1px 3px 0 rgb(50 50 93 / 10%),
    0 1px 2px 0 rgb(50 50 93 / 6%);
  box-shadow: 0 1px 3px 0 rgb(50 50 93 / 10%), 0 1px 2px 0 rgb(50 50 93 / 6%);
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

colgroup {
  display: table-column-group;
}

col {
  display: table-column;
}

thead {
  display: table-header-group;
  vertical-align: middle;
  border-color: inherit;
}

tr {
  display: table-row;
  vertical-align: inherit;
  border-color: inherit;
}

.vgt-table thead th {
  color: #606266;
  vertical-align: bottom;
  border-bottom: 1px solid #dcdfe6;
  padding-right: 1.5em;
  background: -webkit-gradient(
    linear,
    left top,
    left bottom,
    from(#f4f5f8),
    to(#f1f3f6)
  );
  background: linear-gradient(#f4f5f8, #f1f3f6);
}

.vgt-table th {
  padding: 0.75em 1.5em 0.75em 0.75em;
  vertical-align: middle;
  position: relative;
}

th {
  display: table-cell;
  vertical-align: inherit;
  font-weight: bold;
  text-align: -internal-center;
}

.vgt-responsive {
  width: 100%;
  overflow-x: auto;
  position: relative;
}

tbody {
  display: table-row-group;
  vertical-align: middle;
  border-color: inherit;
}

tr {
  display: table-row;
  vertical-align: inherit;
  border-color: inherit;
}

table.vgt-table td {
  padding: 0.75em 0.75em 0.75em 0.75em;
  vertical-align: top;
  border-bottom: 1px solid #dcdfe6;
  color: #606266;
}

td {
  display: table-cell;
  vertical-align: inherit;
}
</style>
>
