<template>
  <div class="hello pt-2">
    <div class="card shadow mb-3 d-print-none" v-show="familySeed.slice(0, 1) === 'X'">
      <div class="card-header"><b>Please enter your secret numbers</b></div>
      <div class="card-body">
        <div class="row pb-1" v-for="i in Object.keys(secret)" v-bind:key="i">
          <div class="col-3 col-md-4 text-right"><b class="text-primary pt-1 d-block">{{ 'ABCDEFGH'.slice(i).slice(0, 1) }}</b></div>
          <div class="col-8 col-md-5"><input :class="{ 'is-valid': checkChecksum(i), 'is-invalid': checkChecksum(i) === false }" maxlength="6" v-model="secret[i]" type="text" class="form-control form-control-sm text-secondary" placeholder="XXXXXX (Please enter)" /></div>
        </div>
      </div>
    </div>
    <div class="text-center" v-show="familySeed.slice(0, 1) !== 'X'">
      <b>Account address (public)</b>
      <br />
      <code class="generated h6 font-weight-bold px-2 text-primary d-inline-block mb-2" v-clipboard:copy="'Account: ' + account">{{ account }}</code>
      <br />
      <br />
      <b>Account secret (for your eyes only)</b>
      <br />
      <small>
        <b>Family Seed</b> (Alternative but common secret format)
        <br />
        <code class="generated px-2 text-danger d-inline-block mb-2" v-clipboard:copy="'Family Seed Secret (keep safe!): ' + familySeed">
          {{ familySeed }}
        </code>
        <small class="d-block mt-3"><b class="text-muted">Raw HEX private key</b></small>
        <small><small><small><code class="generated px-2 text-muted d-inline-block mb-2" v-clipboard:copy="'Raw private key (keep safe!): ' + hexSecret">
          {{ hexSecret }}
        </code></small></small></small>
      </small>
    </div>
    <div class="mt-4 text-center d-print-none" v-show="familySeed.slice(0, 1) !== 'X'">
      <button @click="print()" class="font-weight-bold btn btn btn-dark">Print this (unsafe!) <small>- Better write down &amp; test</small></button>
    </div>
  </div>
</template>

<script>
import Vue from 'vue'
import VueClipboard from 'vue-clipboard2'
// import XrplKeyPairs from 'ripple-keypairs'
import { Account, Utils } from 'xrpl-secret-numbers'

Vue.use(VueClipboard)

export default {
  name: 'Derive',
  methods: {
    print () {
      window.print()
    },
    checkChecksum (i) {
      try {
        return Utils.checkChecksum(i, this.secret[i])
      } catch (e) {}
    },
    calc () {
      const account = new Account(this.secret)
      this.account = account.account.address
      this.familySeed = account.account.familySeed
      this.hexSecret = account.account.keypair.privateKey
    }
  },
  watch: {
    secret () {
      if (Object.keys(this.secret).filter(i => { return this.checkChecksum(i) }).length === 8) {
        this.calc()
      } else {
        this.account = 'XXXXXXXXXXXXXXXXXXXXXXXXXXX'
        this.familySeed = 'XXXXXXXXXXXXXXXXXXXXXXXXXXX'
        this.hexSecret = 'X'.repeat('66')
      }
    }
  },
  data () {
    return {
      account: 'XXXXXXXXXXXXXXXXXXXXXXXXXXX',
      secret: ['', '', '', '', '', '', '', ''],
      familySeed: 'XXXXXXXXXXXXXXXXXXXXXXXXXXX',
      hexSecret: 'X'.repeat('66')
    }
  },
  computed: {
  }
}
</script>

<style scoped lang="scss">
  input[type='text'] {
    font-weight: bold;
  }
  code {
    cursor: pointer;
    letter-spacing: .1em;
    font-size: 1.5em;
    &:active {
      color: white !important;
      background-color: rgba(0, 0, 0, .8);
      outline: 0;
      box-shadow: 0 0 0 3px rgba(0, 123, 255, .5);
      border-radius: 4px;
      z-index: 10;
      position: relative;
      &:before {
        content: 'Copied! (Unsafe!)';
        background-color: rgba(200, 0, 0, .9);
        padding: 1px 4px;
        border-radius: 4px;
        display: block;
        position: absolute;
        color: white;
        font-weight: bold;
        border: 1px solid rgba(0, 0, 0, .5);
        font-size: 12px;
        margin-top: -28px;
        margin-left: -10px;
        letter-spacing: normal;
      }
    }
  }
</style>
