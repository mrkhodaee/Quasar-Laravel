<template>
  <q-page padding>
    <div class="row justify-center">
      <div class="col-xs-12 col-sm-10 col-md-8 col-lg-6 q-gutter-md">
        <q-input
          rounded
          outlined
          placeholder="Enter your email"
          label="Email"
          type="email"
          v-model="email"
        ></q-input>
        <q-input
          rounded
          outlined
          placeholder="Enter your password"
          label="Password"
          type="password"
          v-model="password"
        ></q-input>
        <q-btn class="full-width" color="primary" rounded outline
          >showEmail</q-btn
        >
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { ref } from "vue";

const email = ref("");
const password = ref("");

defineOptions({
  name: "LoginPage",
});
</script>
