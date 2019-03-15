<template>
  <div class="table">
    <div class="thead">
      <span
        class="th"
        v-for="header in headers"
        :key="header"
        :class="'cell-' + headers.length"
      >
        {{ header }}
      </span>
      <span class="th" :class="'cell-' + headers.length">
        {{ countname }}
      </span>
    </div>
    <div class="tr" v-if="headers.length == 0">
      {{ entries.length }}
    </div>
    <div v-for="(entry, prop) in groupedEntries" :key="prop" v-else>
      <div class="tr">
        <div class="td" :class="'cell-' + headers.length">
          <span>{{ prop }}</span>
        </div>
        <RecursiveCell :entry="entry" :level="headers.length - 1" />
      </div>
    </div>
  </div>
</template>

<script>
import RecursiveCell from "./RecursiveCell.vue";
import groupBy from "json-groupby";

export default {
  name: "GroupedTable",
  components: {
    RecursiveCell
  },
  props: {
    headers: {
      type: Array,
      default: () => []
    },
    entries: {
      type: Array,
      default: () => []
    },
    countname: {
      type: String,
      default: "Count"
    }
  },
  computed: {
    groupedEntries: function() {
      return groupBy(this.entries, this.headers);
    }
  }
};
</script>

<style lang="scss">
.table {
  width: 100%;
  text-align: center;

  .thead {
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    border-bottom: 2px double;

    .th {
      font-weight: 600;
    }
  }

  .tr {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    border-bottom: 1px solid;

    .td {
      display: flex;
      flex-direction: column;
      justify-content: center;
      align-items: center;

      .tr:last-of-type {
        border: none;
      }
    }
  }

  @for $i from 0 through 10 {
    .cell-#{$i} {
      $width-first: calc(100% / (#{$i} + 1));
      width: #{$width-first};
      & + .td {
        width: calc(100% - #{$width-first});
      }
    }
  }
}
</style>
