<template>
  <v-toolbar app color="blue">
    <v-toolbar-side-icon @click.stop="openLeftDrawer"></v-toolbar-side-icon>
    <v-toolbar-title>ITMAP</v-toolbar-title>
    <v-layout row align-center ml-5 mr-3 style="max-width: 200px">
      <v-text-field placeholder="Search..." single-line append-icon="search" color="white" hide-details></v-text-field>
    </v-layout>
    <!-- <v-chip color='green'>
      <v-avatar @click.stop="addNode">
        <v-icon medium>fas fa-plus-circle</v-icon>
      </v-avatar>
      <span @click.stop="showDetail">{{node}}</span>
    </v-chip> -->
    <v-spacer></v-spacer>
    <v-chip  @click="showUser" @input="logout">
      <v-avatar>
        <img :src="avatar" alt="trevor" :onerror="defaultImage">
      </v-avatar>
      <span v-if="name">{{name}}</span>
      <span v-else>登录</span>
    </v-chip>
    <!-- <v-btn icon @click="openRightDrawer">
      <v-icon>more_vert</v-icon>
    </v-btn> -->
    <v-dialog  v-model="userDialog" max-width="600px" persistent>
      <user @closeUserDialog="closeUserDialog" @openUserDialog="openUserDialog" />
    </v-dialog>
  </v-toolbar>
</template>
<script>
import { mapState } from 'vuex'
import User from '@/views/User'
export default {
  name: 'app-header',
  components: {
    User
  },
  data () {
    return {
      defaultImage: 'this.src="' + require('../assets/it.jpg') + '"',
      userDialog: false,
      show: true
    }
  },
  computed: {
    ...mapState({
      user_id: state => state.user.id,
      name: state => state.user.name,
      avatar: state => state.user.avatar,
      node: state => state.node.name
    })
  },
  methods: {
    openLeftDrawer () {
      this.$emit('openLeftDrawer')
    },
    // openRightDrawer () {
    //   this.$emit('openRightDrawer')
    // },
    showUser () {
      if (!this.user_id) {
        this.$router.push('login')
      } else {
        this.userDialog = true
      }
    },
    logout () {
    },
    openUserDialog () {
      this.userDialog = true
    },
    closeUserDialog () {
      this.userDialog = false
    }

  }
}
</script>
<style scoped>
.chip .avatar {
  cursor: pointer
}
.chip span {
  cursor: pointer
}
.avatar {
  cursor: pointer;
}
</style>
