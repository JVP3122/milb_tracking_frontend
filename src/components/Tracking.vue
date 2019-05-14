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
    name: "Tracking",
    components: {SplitTable},
    props: {
      splitKeys: {
        type: Array,
        required: true,
      },
    },
    data: () => ({
      headers: {
        'Batters': [
          {value: 'Name', align: 'left', sortable: true, text: 'Name'},
          {value: 'G', align: 'left', sortable: true, text: 'G'},
          {value: 'AB', align: 'left', sortable: true, text: 'AB'},
          {value: 'R', align: 'left', sortable: true, text: 'R'},
          {value: 'RBI', align: 'left', sortable: true, text: 'RBI'},
          {value: 'H', align: 'left', sortable: true, text: 'H'},
          {value: '2B', align: 'left', sortable: true, text: '2B'},
          {value: '3B', align: 'left', sortable: true, text: '3B'},
          {value: 'HR', align: 'left', sortable: true, text: 'HR'},
          {value: 'SB', align: 'left', sortable: true, text: 'SB'},
          {value: 'CS', align: 'left', sortable: true, text: 'CS'},
          {value: 'SO', align: 'left', sortable: true, text: 'SO'},
          {value: 'BA', align: 'left', sortable: true, text: 'BA'},
          {value: 'OBP', align: 'left', sortable: true, text: 'OBP'},
          {value: 'OPS', align: 'left', sortable: true, text: 'OPS'},
        ],
        'Pitchers': [
          {value: 'Name', align: 'left', sortable: true, text: 'Name'},
          {value: 'G', align: 'left', sortable: true, text: 'G'},
          {value: 'GS', align: 'left', sortable: true, text: 'GS'},
          {value: 'W', align: 'left', sortable: true, text: 'W'},
          {value: 'L', align: 'left', sortable: true, text: 'L'},
          {value: 'SV', align: 'left', sortable: true, text: 'SV'},
          {value: 'W-L%', align: 'left', sortable: true, text: 'W-L%'},
          {value: 'IP', align: 'left', sortable: true, text: 'IP'},
          {value: 'R', align: 'left', sortable: true, text: 'R'},
          {value: 'ER', align: 'left', sortable: true, text: 'ER'},
          {value: 'H', align: 'left', sortable: true, text: 'H'},
          {value: 'BB', align: 'left', sortable: true, text: 'BB'},
          {value: 'SO', align: 'left', sortable: true, text: 'K'},
          {value: 'ERA', align: 'left', sortable: true, text: 'ERA'},
          {value: 'WHIP', align: 'left', sortable: true, text: 'WHIP'},
          {value: 'SO9', align: 'left', sortable: true, text: 'K/9'},
          {value: 'SO/W', align: 'left', sortable: true, text: 'K/W'},
        ]
      }
    }),
    computed: {
      tracking() { return require('@/assets/output/tracking.json')},
      tableKeys() {
        return Object.keys(this.tracking)
      },
      items() {
        const returnObj = {};
        this.tableKeys.forEach(table => {
          returnObj[table] = {};
          this.splitKeys.forEach(key => {
            returnObj[table][key] = this.tracking[table][key]
          })
        });
        return returnObj
      }
    },
  }
</script>

<style scoped>

</style>