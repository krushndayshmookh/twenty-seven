<template lang="pug">
  q-layout(view="hHh Lpr lff")

    q-header(elevated)
      q-toolbar
        q-btn(flat dense round icon="menu" aria-label="Menu" @click="miniState = !miniState")

        q-toolbar-title Twenty 7

        q-btn(flat dense round icon="settings" aria-label="Menu" @click="rightDrawerOpen = !rightDrawerOpen")
        

    q-drawer(v-model="leftDrawerOpen" show-if-above :mini="miniState" :width="300" :breakpoint="500" bordered)
      q-scroll-area.fit
        q-list(padding)
          q-item(clickable v-ripple)
            q-item-section(avatar)
              q-icon(name="inbox")
            q-item-section
              | Inbox
          q-item(active clickable v-ripple)
            q-item-section(avatar)
              q-icon(name="star")
            q-item-section
              | Star
          q-item(clickable v-ripple)
            q-item-section(avatar)
              q-icon(name="send")
            q-item-section
              | Send
          q-item(clickable v-ripple)
            q-item-section(avatar)
              q-icon(name="drafts")
            q-item-section
              | Drafts


    q-drawer(v-model="rightDrawerOpen" side="right" show-if-above="" :width="250" :breakpoint="500")
      q-scroll-area.fit
        q-list.menu-list(padding="")
          q-item(clickable="" v-ripple="" @click="darkMode = !darkMode")
            q-item-section(avatar="")
              q-icon(name="inbox")
            q-item-section Dark Mode
            q-item-section.absolute-right
              q-toggle(color="green" v-model="darkMode")
          q-item(active="" clickable="" v-ripple="")
            q-item-section(avatar="")
              q-icon(name="star")
            q-item-section
              | Hidden
          q-item(clickable="" v-ripple="")
            q-item-section(avatar="")
              q-icon(name="send")
            q-item-section
              | Send
          q-item(clickable="" v-ripple="")
            q-item-section(avatar="")
              q-icon(name="drafts")
            q-item-section
              | Drafts


    q-page-container
      router-view

</template>

<script>
export default {
  name: 'MainLayout',

  components: {},

  data() {
    return {
      leftDrawerOpen: false,
      rightDrawerOpen: false,
      miniState: true
    }
  },

  computed: {
    darkMode: {
      get: function() {
        return this.$q.dark.isActive
      },
      set: function(val) {
        this.$q.dark.set(val)
      }
    }
  },
  methods: {
    
  }
}
</script>
