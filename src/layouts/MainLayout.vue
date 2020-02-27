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
          q-item(v-for="(conversation, index) in conversations" :key="conversation.id" clickable="" v-ripple="" @click="currentConversationIndex = index")
            q-item-section(avatar="")
              q-avatar
                img(:src="conversation.avatar")
            q-item-section
              q-item-label(lines="1")
                | {{ conversation.person }}
              q-item-label.conversation__summary(caption="")
                q-icon(name="check" v-if="conversation.sent")
                  q-icon(name="not_interested" v-if="conversation.deleted")
                    | {{ conversation.caption }}
            q-item-section(side="")
              q-item-label(caption="")
                | {{ conversation.time }}
              q-icon(name="keyboard_arrow_down")



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
              q-btn(color="primary" label="Trigger" @click="trigger")
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
    .q-pa-md
      q-ajax-bar(ref="bar" position="bottom" color="accent" size="10px" skip-hijack="")

</template>

<script>
export default {
  name: 'MainLayout',

  components: {},

  data() {
    return {
      leftDrawerOpen: false,
      rightDrawerOpen: false,
      miniState: true,currentConversationIndex: 0,
      conversations: [
        {
          id: 1,
          person: 'Razvan Stoenescu',
          avatar: 'https://cdn.quasar.dev/team/razvan_stoenescu.jpeg',
          caption: 'I\'m working on Quasar!',
          time: '15:00',
          sent: true
        },
        {
          id: 2,
          person: 'Dan Popescu',
          avatar: 'https://cdn.quasar.dev/team/dan_popescu.jpg',
          caption: 'I\'m working on Quasar!',
          time: '16:00',
          sent: true
        },
        {
          id: 3,
          person: 'Jeff Galbraith',
          avatar: 'https://cdn.quasar.dev/team/jeff_galbraith.jpg',
          caption: 'I\'m working on Quasar!',
          time: '18:00',
          sent: true
        },
        {
          id: 4,
          person: 'Allan Gaunt',
          avatar: 'https://cdn.quasar.dev/team/allan_gaunt.png',
          caption: 'I\'m working on Quasar!',
          time: '17:00',
          sent: true
        }
      ]
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
    // we manually trigger it (this is not needed if we
    // don't skip Ajax calls hijacking)
    trigger () {
      const bar = this.$refs.bar

      bar.start()

      this.timer = setTimeout(() => {
        if (this.$refs.bar) {
          this.$refs.bar.stop()
        }
      }, Math.random() * 3000 + 1000)
    }
 
  }
}
</script>
