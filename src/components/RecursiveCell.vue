<template>
  <div class="td">
    <span v-if="entry.length">{{ entry.length }}</span>
    <div class="tr" v-for="key in Object.keys(entry)" :key="key" v-else>
      <div class="td" :class="'cell-' + level">
        <span>{{ key }}</span>
      </div>
      <RecursiveCell :entry="entry[key]" :level="level - 1" />
    </div>
  </div>
</template>

<script>
export default {
  name: "RecursiveCell",
  props: ["entry", "level"]
};
</script>
