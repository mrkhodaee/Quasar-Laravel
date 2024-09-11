<template>
  <q-page padding>
    <div class="row justify-center">
      <div class="col-xs-12 col-sm-10 col-md-8 col-lg-6 q-gutter-md">
        <q-input
          class="full-width"
          rounded
          outlined
          placeholder="Enter your email"
          label="Email"
          type="email"
          hint="حداقل باید 10 کاراکتر باشه."
          lazy-rules
          ref="emailRef"
          :rules="[
            (val) => !!val || 'الزامی است.',
            (val) => val.length >= 10 || 'حداقل باید 10 کاراکتر باشه.',
          ]"
          v-model="email"
        ></q-input>
        <q-input
          class="full-width"
          rounded
          outlined
          placeholder="Enter your password"
          label="Password"
          type="password"
          hint="از 5 کاراکتر نگذرد"
          ref="passwordRef"
          lazy-rules
          v-model="password"
          :rules="[
            (val) => !!val || 'الزامی است.',
            (val) => val.length <= 5 || 'حداکثر باید 5 کاراکتر باشه.',
          ]"
        ></q-input>
        <q-btn
          class="full-width q-py-sm"
          label="showEmail"
          color="primary"
          rounded
          outline
          icon="security"
          @click="login"
        />
      </div>
    </div>
  </q-page>
</template>

<script setup>
import { useQuasar } from "quasar";
import { api } from "src/boot/axios";
import { ref } from "vue";

const email = ref("");
const password = ref("");
const emailRef = ref();
const passwordRef = ref();
const clientId = ref(2);
const clientSecret = ref("uR0pvhCGc6blWrkyXnmx9AFZpiITI6eT6SiSvwBZ");
const q = useQuasar();
function login() {
  // validation quasar
  emailRef.value.validate();
  passwordRef.value.validate();
  if (emailRef.value.hasError || passwordRef.value.hasError) {
    console.log(1);

    q.notify({
      icon: "warning",
      position: "top",
      color: "amber",
      message: "Error",
    });
  } else {
    api
      .post("oauth/token", {
        grant_type: "password",
        client_id: clientId.value,
        client_secret: clientSecret.value,
        username: email.value,
        password: password.value,
        scope: "*",
      })
      .then((r) => {
        console.log(r.data);
      });
  }
}

defineOptions({
  name: "LoginPage",
});
</script>
