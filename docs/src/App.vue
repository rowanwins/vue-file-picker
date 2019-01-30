<template>
  <div id="app">
    <h2>Example</h2>
    <file-picker
      id="filePicker"
      :allow-multiple="false"
      @vfp-file-added="fileAdded"
    >
      <svg
        slot="icon"
        height="40"
        viewBox="0 0 48 48"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M18 32h12v-12h8l-14-14-14 14h8zm-8 4h28v4h-28z"
          fill="#CACFD2"
        />
      </svg>
    </file-picker>

    <h2>Usage</h2>
    <pre>
      {{ snippet }}
    </pre>
  </div>
</template>

<script>

import filePicker from '../../src/filePicker.vue'

export default {
  name: 'App',
  components: {
    filePicker
  },
  data () {
    return {
      snippet: `
    <file-picker id="filePicker" v-on:vfp-file-added="fileAdded">
      <svg slot="icon" height="40" viewBox="0 0 48 48" xmlns="http://www.w3.org/2000/svg">
          <path d="M18 32h12v-12h8l-14-14-14 14h8zm-8 4h28v4h-28z" fill="#CACFD2"/>
      </svg>
    </file-picker>`
    }
  },
  methods: {
    fileAdded: function (fileList) {
      console.log('vfp:', fileList)
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=PT+Sans:400');
@import url('https://fonts.googleapis.com/css?family=PT+Sans+Narrow:700');

#app {
  padding: 50px 100px;
  font-family: 'PT Sans', sans-serif;

  h2{
    margin-bottom: 10px;
    margin-top: 30px;
    font-size: 1.3rem;
    font-family: 'PT Sans Narrow', sans-serif;
    letter-spacing: 0.1rem;
  }
  h3{
    font-size: 1.1rem;
  }
}
pre{
  background: #F8F9F9;
  border: 1px solid #E5E7E9;
}
</style>
