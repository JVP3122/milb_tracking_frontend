<template>
  <v-data-table
    :headers="headers"
    :items="items"
  >
    <template v-slot:items="props">
      <td
        v-for="header in headers"
        :key="header.value"
      >
        {{ props.item[header.value] }}
      </td>
    </template>
  </v-data-table>
</template>

<script>
  export default {
    name: "SplitTable",
    props: {
      items: {
        type: Array,
        required: true
      },
      headers: {
        type: Array,
        required: true
      }
    },
  }
</script>

<style scoped>

</style>