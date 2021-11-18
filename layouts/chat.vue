<template>
  <v-app app>
    <v-navigation-drawer
      v-model="drawer"
      app
      hide-overlay
      :permanent="drawer"
      mobile-breakpoint="700"
    >
      <v-card class="mx-auto" max-width="500">
        <v-toolbar>
          <v-toolbar-title>New Chat</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-btn icon>
            <v-icon>mdi-magnify</v-icon>
          </v-btn>
        </v-toolbar>
        <UserList />
      </v-card>
    </v-navigation-drawer>
    <v-app-bar app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>
      <v-btn icon @click="exit">
        <v-icon>mdi-arrow-left</v-icon>
      </v-btn>
      <v-toolbar-title>
        {{ chatTitle }}
      </v-toolbar-title>
    </v-app-bar>
    <v-main>
      <div class="content">
        <nuxt />
      </div>
    </v-main>
  </v-app>
</template>
<script>
import { mapState, mapMutations } from 'vuex'
import UserList from '~/components/UserList'

export default {
  components: { UserList },
  data() {
    return {
      title: 'Vue-App',
      drawer: true,
      activeUser: {},
    }
  },
  computed: {
    ...mapState(['user']),
    updateDate() {
      return this.date && this.date.toLocaleString()
    },
    chatTitle() {
      return `${this.title} | Чат комнаты ${this.user.room}`
    },
  },
  mounted() {
    // this.setUpdateDate()
  },
  methods: {
    ...mapMutations(['clearData']),
    // setUpdateDate() {
    //   setInterval(() => {
    //     this.date = new Date()
    //   }, 500)
    // },
    exit() {
      this.$root.$socket.emit('userLeft', this.user.id, () => {
        this.$router.push('/?message=leftChat')
        this.clearData()
      })
    },
  },
}
</script>
<style scoped lang="scss">
@import '../assets/variables.scss';
.content {
  height: 100%;
}
i.icon-active {
  color: $color1;
}
</style>
