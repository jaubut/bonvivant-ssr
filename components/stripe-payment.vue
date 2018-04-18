<template>
  <div id='app'>
    <card class='stripe-card'
      :class='{ complete }'
      stripe='pk_test_IngCLTu9rvg3MZGc40jmhaOc'
      :options='stripeOptions'
      @change='complete = $event.complete'
    />
    <button class='pay-with-stripe' @click='pay' :disabled='!complete'>Pay with credit card</button>
  </div>
</template>

<script>
import { Card, createToken } from 'vue-stripe-elements-plus'

export default {
  data () {
    return {
      complete: false,
      stripeOptions: {
        // see https://stripe.com/docs/stripe.js#element-options for details
      }
    }
  },

  components: { Card },

  methods: {
    pay () {
      // createToken returns a Promise which resolves in a result object with
      // either a token or an error key.
      // See https://stripe.com/docs/api#tokens for the token object.
      // See https://stripe.com/docs/api#errors for the error object.
      // More general https://stripe.com/docs/stripe.js#stripe-create-token.
      createToken().then(data => console.log(data.token))
    }
  }
}
</script>

<style scoped>
.stripe-card {
  width: 300px;
}
.stripe-card.complete {
  border-color: green;
}
.pay-with-stripe {
  display: inline-block;
  height: 40px;
  line-height: 40px;
  padding: 0 14px;
  background: #fff;
  border-radius: 4px;
  border: none;
  font-size: 15px;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: .025em;
  color: #6772e5;
  text-decoration: none;
  -webkit-transition: all .15s ease;
  transition: all .15s ease;
  white-space: nowrap;
  box-shadow: 0 4px 6px rgba(50,50,93,.11), 0 1px 3px rgba(0,0,0,.08);
  cursor: pointer;
}
.pay-with-stripe:hover {
  color: #7795f8;
  transform: translateY(-1px);
  box-shadow: 0 7px 14px rgba(50,50,93,.1), 0 3px 6px rgba(0,0,0,.08);
}
</style>