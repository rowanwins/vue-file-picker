<template>
  <div id="app">
    <h2>Example</h2>
    <file-picker
      id="filePicker"
      :allow-multiple="false"
      @vfp-file-added="fileAdded"
    />
    <h3>Usage</h3>
    <pre>
      {{ snippet }}
    </pre>

    <h2>Complex Example</h2>
    <file-picker
      v-if="userHasPickedNoFiles"
      id="filePicker"
      :allow-multiple="false"
      @vfp-file-added="fileAdded2"
    />
    <p v-else>
      User did something and I got files which I can present however I want!
    </p>
    <h3>Usage</h3>
    <pre>
      {{ snippet2 }}
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
    <file-picker id="filePicker" v-on:vfp-file-added="fileAdded"></file-picker>`,
      snippet2: `
    <file-picker v-if="userHasPickedNoFiles" id="filePicker" v-on:vfp-file-added="fileAdded"></file-picker>
    <p v-else>User did something and I got files which I can present however I want!</p>`,
      userHasPickedNoFiles: true
    }
  },
  methods: {
    fileAdded: function (fileList) {
      console.log('vfp:', fileList)
    },
    fileAdded2: function () {
      this.userHasPickedNoFiles = false
    }
  }
}
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css?family=PT+Sans:400');
@import url('https://fonts.googleapis.com/css?family=PT+Sans+Narrow:700');

#app {
  padding: 0px 100px;
  font-family: 'PT Sans', sans-serif;

  h2{
    margin-bottom: 10px;
    margin-top: 100px;
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
