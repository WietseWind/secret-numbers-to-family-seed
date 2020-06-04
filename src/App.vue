<template>
  <div id="app" class="container pt-3 pb-5">
    <h3>XRPL Secret Numbers to Family Seed (s...)</h3>
    <p>Generate a s... Family Seed (Secret) to use in other XRPL tools if you only have "Secret Numbers"</p>
    <p class="alert alert-danger">
      If you generated your Secret Numbers in a secure client like XUMM, converting your Secret Numbers to
      a family seed to use in 3rd party applications MAY BE A RISK! If those 3rd party applications are
      insecure, or you enter your Family Seed (secret) in an unsecure environment, or copy/paste on a
      compromised device, you are at risk of LOSING ALL YOUR FUNDS.
    </p>
    <Derive />

    <div class="mt-5 pt-3">
      <div class="text-center">
        By <a class="btn btn-primary btn-sm py-1" href="https://twitter.com/WietseWind" target="_blank"><b>@WietseWind</b></a>
        <span class="d-print-none">
          - <a class="btn btn-primary btn-sm py-1" href="https://github.com/WietseWind/secret-numbers-to-family-seed/releases" target="_blank"><b>Download (Github)</b></a>
          - <a class="btn btn-outline-primary btn-sm py-1" href="https://github.com/WietseWind/secret-numbers-to-family-seed" target="_blank"><b>Source code (Github)</b></a>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import Derive from './components/Derive.vue'

export default {
  name: 'App',
  components: {
    Derive
  },
  data () {
    return {
    }
  },
  watch: {
  },
  methods: {
  },
  computed: {
  },
  mounted () {
  }
}
</script>

<style lang="scss">
  @media print {
    .d-print-none {
      display: none!important;
    }
  }
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
  }
  html, body {
    -webkit-touch-callout: none; /* iOS Safari */
      -webkit-user-select: none; /* Safari */
      -khtml-user-select: none; /* Konqueror HTML */
        -moz-user-select: none; /* Old versions of Firefox */
          -ms-user-select: none; /* Internet Explorer/Edge */
              user-select: none; /* Non-prefixed version, currently
                                    supported by Chrome, Edge, Opera and Firefox */
  }
</style>
