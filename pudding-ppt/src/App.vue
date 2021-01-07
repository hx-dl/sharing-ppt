<template>
  <div id="app">
    <mark-display :src="pptPath" @title="setTitle" keyboard-ctrl url-hash-ctrl support-preview auto-blank-target ref="display" />
  </div>
</template>
<script>
import Hammer from 'hammerjs'
import MarkDisplay from 'vue-mark-display'
const pptPath = './ppt.txt'
export default {
  components: { MarkDisplay },
  data: () => ({ pptPath }),
  mounted() {
    const mc = new Hammer(this.$el)
    const display = this.$refs.display
    mc.on('swipe', (event) => {
      if (event.pointerType === 'mouse') {
        return
      }
      switch (event.direction) {
        case Hammer.DIRECTION_LEFT:
          display.goNext()
          return
        case Hammer.DIRECTION_RIGHT:
          display.goPrev()
          return
      }
    })
  },
  methods: {
    setTitle({ title }) {
      document.title = [title, 'Example'].filter(Boolean).join(' - ')
    }
  }
}
</script>
<style>
.mark-display {
  font-size: 2.2vw !important;
}
body {
  margin: 0;
  overflow: hidden;
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #f5f5f5;
  text-shadow: 0 0 0.25em #ccc;
  line-height: 1.25;
}
h1,
h2,
h3,
h4,
h5,
h6 {
  margin: 0.25em 0;
  font-weight: 500;
}
p {
  margin: 0.25em 0;
}
li {
  text-align: initial;
}
blockquote {
  font-size: 0.6em;
  text-align: initial;
  background-color: rgba(127, 127, 127, 0.2);
  padding: 0.25em 1em;
  border-radius: 0.25em;
}
pre {
  text-align: initial;
  background-color: rgba(255, 255, 255, 0.8);
  border-radius: 0.5vw;
  padding: 0 0.125em;
}
img {
  max-width: 100%;
  max-height: 80vh;
}
a {
  font-size: 0.75em;
  padding: 0.125em 0.25em;
  background-color: gray;
  color: white;
  border-radius: 0.25em;
  transition: all 0.3s;
  text-decoration: none;
}
a:hover {
  background-color: rgb(37, 143, 241);
  color: white;
}
small {
  font-size: 0.6em;
}
strong {
  color: red;
}
em {
  color: rgb(37, 143, 241);
}
s,
strike {
  color: gray;
}
code {
  font-size: 0.75em;
}
mark {
  border-radius: 0.5vw;
  padding: 0 0.125em;
}
table {
  border-collapse: collapse;
  margin: 0.25em 0;
  background-color: white;
  font-size: inherit;
}
th,
td {
  border: 1px solid gray;
  padding: 0.25em;
}
thead {
  background-color: #f0f0f0;
}
tbody > tr:nth-child(2n) {
  background-color: #f0f0f0;
}
hr {
  width: 90%;
  border-width: 2px;
  border-style: dashed;
}
</style>
