<template>
  <div class="wrapper">
    <h1>Tweet {{ msg }} without duplicated entry</h1>
    <div class="tweet-button-wrapper">
      <a class="tweet-button" @click="setUrl(msg)" :href="url" target="_blank">{{ msg }}</a>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OhishiIzumiSuki',
  props: {
    msg: String
  },
  data() {
    return {
      url: ''
    }
  },
  mounted() {
    this.$nextTick( function() {
      this.setUrl(this.msg)
    })
  },
  methods: {
    randomRange(start, end) {
      return Math.round(Math.random() * (end - start)) + start
    },
    generateNBSP(width, result = '') {
      if (!width) return result
      return this.generateNBSP(--width, result += '\u200B')
    },
    insertNBSP(text, result = '') {
      if (!text) return result
      result += text[0] + this.generateNBSP(this.randomRange(0, 20))
      return this.insertNBSP(text.slice(1), result)
    },
    setUrl(text) {
      this.url = 'https://twitter.com/intent/tweet?text=' + encodeURI(this.insertNBSP(text))
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1 {
  margin-bottom: 40px;
}

.tweet-button {
  border-radius: 4px;
  background-color: navy;
  color: white;
  padding: 10px;
  font-weight: bold;
  text-decoration: none;
}
</style>
