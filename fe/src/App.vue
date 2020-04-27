<template>
  <v-app>
    <v-navigation-drawer
      persistent
      :clipped="clipped"
      :mini-variant="miniVariant"
      color="primary"
      v-model="drawer"
      enable-resize-watcher
      fixed
      dark
      app
    >
      <v-list>
        <v-list-item two-line :class="miniVariant && 'px-0'">
          <v-list-item-avatar>
            <img src="https://randomuser.me/api/portraits/men/81.jpg" alt="">
          </v-list-item-avatar>

          <v-list-item-content>
            <v-list-item-title>게스트</v-list-item-title>
            <v-list-item-subtitle>우리, 졸업할 수 있을까?</v-list-item-subtitle>
          </v-list-item-content>
        </v-list-item>

        <v-divider/>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      app
      :clipped-left="clipped">
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"/>
      <v-toolbar-title v-text="title"/>
      <v-spacer/>
    </v-app-bar>
      class="overflow-hidden">
      <v-content>
        <router-view/>
      </v-content>
  </v-app>
</template>

<script>
export default {
  name: 'App',
  components: {
  },

  data: () => ({
    clipped: false,
    drawer: false,
    fixed: false,
    customIcon: 'mdi-folder',
    customIcon2: 'mdi-account-circle',
    items: [{
      icon: 'mdi-view-dashboard',
      title: '달성도 확인',
      to: {
        path: '/'
      }
    },
    {
      icon: 'mdi-home',
      title: '정보',
      to: {
        path: '/info'
      }
    },
    {
      icon: 'mdi-help-circle',
      title: '도움말',
      to: {
        path: '/help'
      }
    },
    {
      icon: 'mdi-account-star',
      title: '개발자',
      to: {
        path: '/credit'
      }
    }
    ],
    miniVariant: false,
    right: false,
    rightDrawer: false,
    title: '슬기로운 학교생활',
    permanent: true,
    background: false,
    expandOnHover: false,
    color: 'primary',
    colors: [
      'primary',
      'blue',
      'success',
      'red',
      'teal'
    ],
    isMobile: false
  }),
  computed: {
  },

  beforeDestroy () {
    if (typeof window !== 'undefined') {
      window.removeEventListener('resize', this.onResize, { passive: true })
    }
  },

  mounted () {
    this.onResize()
    window.addEventListener('resize', this.onResize, { passive: true })
  },

  methods: {
    onResize () {
      this.isMobile = window.innerWidth < 600
    }
  }
}
</script>
