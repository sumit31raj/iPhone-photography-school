<script>
  export default {
    name: 'modal',
    data() {
    	return {
        showError : '',
        activeLabel: '',
        customerEmail : '',
        reg: /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,24}))$/
    		}
    	},
    methods: {
      close() {
        this.$emit('close');
      },
      togglePicker() {
        this.activeLabel = 'active--label';
      },
      removePicker() {
        this.activeLabel = (this.customerEmail.trim()) ? 'active--label' : '';
      },

      checkEmail() { 
        this.showError = (this.reg.test(this.customerEmail)) ? '' : 'error';         
      },

    },
  };
</script>

<template>
  <div class="modal--backdrop">
    <div class="modal">
      <header class="modal--header">
        Step1 of 2
        <button type="button" class="btn--close" @click="close">
          <img src="images/close.png">
        </button>
      </header>
      <section class="modal--body">
        <div class="progress--bar">
          <div class="progress" style="width: 50%;"> </div>
        </div>
          <h1> Enter Your Email To Get <span> FREE</span> iPhone Photography Email Tips:</h1>
          <div :class="['input--box', showError]">
            <label :class="['text--label', activeLabel]">Enter your email here</label>
            <input type="email" v-model="customerEmail" class="input--field" @focus="togglePicker()"  @blur="removePicker"  @keypress="checkEmail" required>
          </div>
          <button class="btn btn--send btn--block"> Send Me The Tips » </button>
       </section>
    </div>
  </div>
</template>
