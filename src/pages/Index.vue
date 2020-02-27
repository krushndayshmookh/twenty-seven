<template lang="pug">
  q-page
    .q-pt-sm
      q-input.q-ma-xs(outlined readonly v-model="partnerMessage" placeholder="Partner")

      q-input.q-ma-xs(outlined v-model="selfMessage" placeholder="You")
        template(v-slot:append)
          q-icon(v-if="selfMessage !== ''" name="close" @click="selfMessage = ''" class="cursor-pointer")

      .q-ma-xs
        q-badge(:color="connectionStatus ? 'green' : 'orange'" :label="connectionStatus ? 'Online' : 'Offline'")

</template>

<script>
import _ from 'lodash'
import io from 'socket.io-client'

export default {
  name: 'PageIndex',
  data() {
    return {
      selfMessage: '',
      partnerMessage: '',
      connectionStatus: false
    }
  },
  watch: {
    selfMessage(val) {
      this.debouncedSendMessage()
    }
  },
  created() {
    this.debouncedSendMessage = _.debounce(this.sendMessage, 500)
  },
  mounted() {
    this.socket = io.connect('https://twenty-seven.herokuapp.com/')
    this.attachSocketListeners()
  },
  methods: {
    sendMessage() {
      this.socket.emit('msg', {
        body: this.selfMessage,
        to: 'krushn',
        from: 'daffy'
      })
    },
    attachSocketListeners() {
      const vm = this

      this.socket.on('connect', function() {
        console.log('Socket connected.')
        vm.connectionStatus = true
        vm.doSocketLogin()
      })

      this.socket.on('disconnect', function() {
        console.log('Socket disconnected.')
        vm.connectionStatus = false
      })

      this.socket.on('msg', this.handleIncomingMessage)
      // this.socket.on('stock data downloaded', function(data) {
      //   vm.download.count = data.downloadCount
      //   if (vm.download.count == vm.download.total) vm.download.status = false
      //   console.log(vm.download, data)
      // })
    },
    doSocketLogin() {},
    handleIncomingMessage(data) {
      console.log(data)
      this.partnerMessage = data.body
    }
  }
}
</script>
