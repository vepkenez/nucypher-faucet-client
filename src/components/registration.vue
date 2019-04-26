<template>
    <b-jumbotron class="mechanics" lead="To receive tokens, register your public key here">
        <b-form @submit.prevent="onSubmit">
        <b-form-input v-model="address" placeholder="Your public key"></b-form-input>
        <b-btn class="mt-3" variant="primary" type="submit">ok</b-btn>
        </b-form>
        <b-alert class="mt-3" show v-if="error" variant="danger">{{error}}</b-alert>
        <b-alert class="mt-3" show v-if="success" variant="success">{{address}} successfully registered.</b-alert>
    </b-jumbotron>
</template>

<script>
import http from '@/http';
export default {
  data() {
    return {
      address: '',
      success: false,
      error: null,
    };
  },
  methods: {
    onSubmit(){
      http.post('register', { address: this.address }).then((res) => {
        this.error = null;
        this.success = true;
      }).catch((err) => {
        this.success = false;
        this.error = err.response.data;
      });
    },
  },
}
</script>

<style scoped>


</style>
