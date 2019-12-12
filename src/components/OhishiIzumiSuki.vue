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
    generateZWSP(width, result = '') {
      if (!width) return result
      return this.generateZWSP(--width, result += '\u200B')
    },
    insertZWSP(text, result = '') {
      if (!text) return result
      result += text[0] + this.generateZWSP(this.randomRange(0, 20))
      return this.insertZWSP(text.slice(1), result)
    },
    countBytes(text) {
      return encodeURIComponent(text).replace(/%../g,"x").length
    },
    setUrl(text) {
      let content = this.insertZWSP(text)
      this.url = "https://twitter.com/intent/tweet?text=" + encodeURI(content + "\nhttps://ohishi-izumi-suki.herokuapp.com")
      console.log(`「${content}」は${content.length}文字(${this.countBytes(content)}bytes)です`)
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
