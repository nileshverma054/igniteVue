/* eslint-disable no-trailing-spaces */
<template>
  <v-app>
    <v-main>
      <v-app-bar
        app
        color="white"
        elevation="1"
      >
        <v-app-bar-nav-icon @click="drawer = !drawer" class="hidden-sm-and-up"></v-app-bar-nav-icon>
        <v-toolbar-title>Dashboard</v-toolbar-title>
        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon>mdi-cog</v-icon>
        </v-btn>
      </v-app-bar>
      <!-- Page container -->
      <v-container>
        <events/>
      </v-container>
      <!-- :expand-on-hover= "$vuetify.breakpoint.mdAndUp" -->
      <v-navigation-drawer
        v-model="drawer"
        app
        :permanent= "$vuetify.breakpoint.smAndUp"
        :temporary= "$vuetify.breakpoint.xs"
        active-class="orange--text text--accent-4"
      >
        <v-list class="text-center">
          <v-avatar
            color="orange"
            size="90"
          >
            <span class="white--text headline">{{loggedInUser.avatar}}</span>
          </v-avatar>
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title class="title">
                {{loggedInUser.name}}
              </v-list-item-title>
              <v-list-item-subtitle>{{loggedInUser.email}}</v-list-item-subtitle>
            </v-list-item-content>
          </v-list-item>
          <v-chip
                class="ma-2"
                color=""
                text-color=""
              >
                {{loggedInUser.userType}}
              </v-chip>
        </v-list>
        <v-divider></v-divider>
        <!-- sidebar items -->
        <v-list
          nav
          dense
          rounded
        >
          <v-list-item-group
            v-model="group"
            active-class="dark-orange--text"
          >
            <div
              v-if= "$vuetify.breakpoint.smAndUp"
            >
              <v-list-item
                v-for="item in bottomMenuItems" :key="item.id"
              >
                <v-list-item-icon> <v-icon>{{item.icon}}</v-icon></v-list-item-icon>
                <v-list-item-title>{{item.label}}</v-list-item-title>
              </v-list-item>
              <v-divider class="mx-4 my-2"></v-divider>
            </div>
            <!-- consitent sidebar items -->
            <v-list-item
              v-for="item in sidebMenuItems" :key="item.id"
            >
              <v-list-item-icon><v-icon>{{item.icon}}</v-icon></v-list-item-icon>
              <v-list-item-title>{{item.label}}</v-list-item-title>
            </v-list-item>
          </v-list-item-group>
        </v-list>
      </v-navigation-drawer>
      <v-bottom-navigation
        v-if= "$vuetify.breakpoint.xs"
        class="d-flex justify-space-around"
        fixed
        app
        color="orange"
      >
        <v-btn
          v-for="item in bottomMenuItems" :key="item.id"
        >
          <span>{{item.label}}</span>
          <v-icon>{{item.icon}}</v-icon>
        </v-btn>
      </v-bottom-navigation>
    </v-main>
  </v-app>
</template>

<script>
import Events from './components/events.vue'
// import HelloWorld from './components/HelloWorld.vue'
// console.log('hello')

export default {
  name: 'App',
  mounted () {
    console.log('smup ' + this.$vuetify.breakpoint.smAndUp)
    console.log('smdown ' + this.$vuetify.breakpoint.smAndDown)
    console.log('xs ' + this.$vuetify.breakpoint.xs)
    console.log('md ' + this.$vuetify.breakpoint.md)
    console.log('sm ' + this.$vuetify.breakpoint.md)
  },

  components: {
    Events
    // HelloWorld
  },
  data: () => ({
    drawer: false,
    group: null,
    loggedInUser: {
      name: 'Nilesh Verma',
      email: 'nileshverma054@gmail.com',
      userType: 'Admin',
      avatar: 'NV'
    },
    sidebMenuItems: [
      { id: 'S101', icon: 'mdi-google-analytics', label: 'Analytics' },
      { id: 'S102', icon: 'mdi-account-multiple', label: 'Manage Users' },
      { id: 'S103', icon: 'mdi-logout', label: 'Logout' }
    ],
    bottomMenuItems: [
      { id: 'B101', icon: 'mdi-cube', label: 'Events' },
      { id: 'B102', icon: 'mdi-bookshelf', label: 'Registrations' },
      { id: 'B103', icon: 'mdi-account-plus', label: 'New' }
    ]
  }),
  watch: {
    group () {
      this.drawer = false
    }
  }
}
</script>
