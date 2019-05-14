<template>
  <v-app>
    <v-toolbar app>
      <v-toolbar-title class="headline text-uppercase">
        <span>Vuetify</span>
        <span class="font-weight-light">MATERIAL DESIGN</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-menu offset-y>
        <template v-slot:activator="{ on }">
          <v-btn
            small
            round
            v-on="on"
          >
            <span class="mr-2">Owned</span>
          </v-btn>
        </template>
        <v-list>
          <v-list-tile
            v-for="key in splitKeysArray"
            :key="key"
            @click="goToRoute(key, 'Owned')"
          >
            <v-list-tile-title>{{ key }}</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>
      <v-menu offset-y>
        <template v-slot:activator="{ on }">
          <v-btn
            small
            round
            v-on="on"
          >
            <span class="mr-2">Tracking</span>
          </v-btn>
        </template>
        <v-list>
          <v-list-tile
            v-for="key in splitKeysArray"
            :key="key"
            @click="goToRoute(key, 'Tracking')"
          >
            <v-list-tile-title>{{ key }}</v-list-tile-title>
          </v-list-tile>
        </v-list>
      </v-menu>
    </v-toolbar>
    <v-content>
      <Owned
        v-if="route === 'Owned'"
        :split-keys="splitKeys"
      />
      <Tracking
        v-if="route === 'Tracking'"
        :split-keys="splitKeys"
      />
    </v-content>
  </v-app>
</template>

<script>
  import Owned from "./components/Owned";
  import Tracking from "./components/Tracking";

  export default {
    name: 'App',
    components: {
      Tracking,
      Owned,
    },
    data: () => ({
      route: 'Owned',
      splitKeys: ['Last 28 days'],
      splitKeysArray: [
        'Total',
        'Last 7 days',
        'Last 28 days',
        'Last 90 days',
        'All'
      ],
    }),
    methods: {
      goToRoute(key, route) {
        console.log('key', key)
        console.log('route', route)
        this.splitKeys = key === 'All' ? this.splitKeysArray.filter(e => e !== 'All') : [key];
        this.route = route;
      },
    }
  }
</script>
