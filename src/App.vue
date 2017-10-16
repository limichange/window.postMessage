<template>
  <div id="app">
    <button @click="open">open</button>
  </div>
</template>

<script>
export default {
  name: 'app',
  components: {
  },
  mounted () {
    // 监听消息反馈
    window.addEventListener('message', (event) => {
      console.log('received response:  ', event.data)
    }, false)
  },
  methods: {
    open () {
      // 弹出一个新窗口
      var myPopup = window.open('http://localhost:8080', 'myWindow')

      // 周期性的发送消息
      setInterval(() => {
        var message = 'Hello!  The time is: ' + (new Date().getTime())
        console.log('blog.local:  sending message:  ' + message)
        // send the message and target URI
        myPopup.postMessage(message, 'http://localhost:8080')
      }, 6000)
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
