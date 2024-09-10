<template>
  <q-page class="">
    <q-input
      placeholder="email"
      label="Email"
      type="email"
      class="q-mt-lg"
      rounded
      outlined
      v-model="username"
    />
    <input type="text" />
    <q-input
      placeholder="password"
      label="Password"
      class="q-mt-lg"
      rounded
      outlined
      v-model="password"
    />
    <q-input
      placeholder="confirm password"
      label="Confirm Password"
      class="q-mt-lg"
      rounded
      outlined
      v-model="confirmPassword"
    />
    <q-btn
      class="full-width q-mt-md q-py-sm bg-purple-8"
      color="primary"
      rounded
      @click="register"
      >Register</q-btn
    >

    {{ username }}
  </q-page>
</template>

<script setup>
import { api } from "src/boot/axios";
import { ref } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();
const username = ref("");
const password = ref("");
const confirmPassword = ref("");

function register() {
  if (password.value === confirmPassword.value) {
    api
      .post("api/register", {
        email: username.value,
        password: password.value,
      })
      .then((r) => {
        console.log(r.data);
        if (r.data.status) {
          console.log(1);

          router.push("/login");
        } else {
          alert("prablum");
        }
      });
  }
}
defineOptions({
  name: "IndexPage",
});
</script>
