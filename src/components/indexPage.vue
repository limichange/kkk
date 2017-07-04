<template>
  <div class="hello">
    {{ positionServe }}
    <button @click="ok">OK</button>
  </div>
</template>

<script>
import * as wilddog from 'wilddog'
import phaser from 'phaser-ce'

console.log(phaser)

var config = {
  syncURL: 'https://tbs.wilddogio.com'
}

wilddog.initializeApp(config)
var ref = wilddog.sync().ref()

export default {
  name: 'hello',
  data () {
    return {
      positionServe: {
        x: 0,
        y: 0
      },
      position: {
        x: 0,
        y: 0
      }
    }
  },
  mounted () {
    const self = this
    ref.on('value', (snapshot) => {
      self.positionServe = snapshot.val().position
    })
  },
  methods: {
    ok () {
      const self = this
      ref.set({
        position: {
          x: self.position.x++,
          y: self.position.y++
        }
      })
    }
  }
}
</script>

<style scoped>
</style>
