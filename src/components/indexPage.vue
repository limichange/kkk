<template>
  <div class="hello">
    {{ index }}
    <button @click="ok">OK</button>
  </div>
</template>

<script>
import * as wilddog from 'wilddog'

var config = {
  syncURL: 'https://tbs.wilddogio.com'
}

wilddog.initializeApp(config)
var ref = wilddog.sync().ref()

export default {
  name: 'hello',
  data () {
    return {
      index: 0
    }
  },
  mounted () {
    const self = this
    ref.on('value', (snapshot) => {
      self.index = snapshot.val().index
    })
  },
  methods: {
    ok () {
      const self = this
      ref.set({
        index: self.index++
      })
    }
  }
}
</script>

<style scoped>
</style>
