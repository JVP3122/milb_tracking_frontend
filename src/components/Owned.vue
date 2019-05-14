<template>
  <v-layout row wrap fill-height justify-center>
    <v-flex
      grow
      v-for="table in tableKeys"
      :key="table"
    >
      <v-card flat>
        <v-card-title>
          {{ table }}
        </v-card-title>
        <v-card-text>
          <v-card
            v-for="split in splitKeys"
            :key="split"
            class="my-2"
          >
            <v-card-title>{{split}}</v-card-title>
            <v-card-text>
              <SplitTable
                :items="items[table][split]"
                :headers="headers[table]"
              />
            </v-card-text>
          </v-card>
        </v-card-text>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
  import SplitTable from "./SplitTable";
  export default {
    name: "Owned",
    components: {SplitTable},
    props: {
      splitKeys: {
        type: Array,
        required: true,
      }
    },
    data: () => ({
      headers: {
        'Batters': [
          {value: 'Name', align: 'center', sortable: true, text: 'Name'},
          {value: 'G', align: 'center', sortable: true, text: 'G'},
          {value: 'AB', align: 'center', sortable: true, text: 'AB'},
          {value: 'R', align: 'center', sortable: true, text: 'R'},
          {value: 'RBI', align: 'center', sortable: true, text: 'RBI'},
          {value: 'H', align: 'center', sortable: true, text: 'H'},
          {value: '2B', align: 'center', sortable: true, text: '2B'},
          {value: '3B', align: 'center', sortable: true, text: '3B'},
          {value: 'HR', align: 'center', sortable: true, text: 'HR'},
          {value: 'SB', align: 'center', sortable: true, text: 'SB'},
          {value: 'CS', align: 'center', sortable: true, text: 'CS'},
          {value: 'SO', align: 'center', sortable: true, text: 'SO'},
          {value: 'BA', align: 'center', sortable: true, text: 'BA'},
          {value: 'OBP', align: 'center', sortable: true, text: 'OBP'},
          {value: 'OPS', align: 'center', sortable: true, text: 'OPS'},
        ],
        'Pitchers': [
          {value: 'Name', align: 'center', sortable: true, text: 'Name'},
          {value: 'G', align: 'center', sortable: true, text: 'G'},
          {value: 'GS', align: 'center', sortable: true, text: 'GS'},
          {value: 'W', align: 'center', sortable: true, text: 'W'},
          {value: 'L', align: 'center', sortable: true, text: 'L'},
          {value: 'SV', align: 'center', sortable: true, text: 'SV'},
          {value: 'W-L%', align: 'center', sortable: true, text: 'W-L%'},
          {value: 'IP', align: 'center', sortable: true, text: 'IP'},
          {value: 'R', align: 'center', sortable: true, text: 'R'},
          {value: 'ER', align: 'center', sortable: true, text: 'ER'},
          {value: 'H', align: 'center', sortable: true, text: 'H'},
          {value: 'BB', align: 'center', sortable: true, text: 'BB'},
          {value: 'SO', align: 'center', sortable: true, text: 'K'},
          {value: 'ERA', align: 'center', sortable: true, text: 'ERA'},
          {value: 'WHIP', align: 'center', sortable: true, text: 'WHIP'},
          {value: 'SO9', align: 'center', sortable: true, text: 'K/9'},
          {value: 'SO/W', align: 'center', sortable: true, text: 'K/W'},
        ]
      }
    }),
    computed: {
      owned() { return require('@/assets/output/owned.json')},
      tableKeys() {
        return Object.keys(this.owned)
      },
      items() {
        const returnObj = {};
        this.tableKeys.forEach(table => {
          returnObj[table] = {};
          this.splitKeys.forEach(key => {
            returnObj[table][key] = this.owned[table][key]
          })
        });
        return returnObj
      }
    },
    mounted() {
      console.log('this.splitKeys', this.splitKeys)
    }
  }
</script>

<style scoped>

</style>