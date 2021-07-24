<template>
  <div class="q-pa-md" style="max-width: 400px">
    <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
      <q-input
        filled
        v-model="name"
        label="Account Name *"
        lazy-rules
        :rules="[val => (val && val.length > 0) || 'Please type something']"
      />

      <q-input
        filled
        v-model="email"
        label="Your email *"
        lazy-rules
        :rules="[val => (val && val.length > 0) || 'Please type something']"
      />

      <q-input
        filled
        v-model="password"
        label="Your Password *"
        type="password"
        lazy-rules
        :rules="[
          val => (val && val.length > 8) || 'Provide long enough password'
        ]"
      />
      <q-input
        filled
        v-model="repeated_password"
        label="Repeat Password *"
        type="password"
        lazy-rules
        :rules="[
          val => (val && val == password) || 'Provide same password'
        ]"
      />
      <q-toggle v-model="accept" label="I accept the license and terms" />

      <div>
        <q-btn label="Submit" type="submit" color="primary" />
        <q-btn
          label="Reset"
          type="reset"
          color="primary"
          flat
          class="q-ml-sm"
        />
      </div>
    </q-form>
  </div>
</template>

<script>
import { useQuasar } from "quasar";
import { ref } from "vue";

export default {
  setup() {
    const $q = useQuasar();

    const name = ref(null);
    const email = ref(null);
    const password = ref(null);
    const repeated_password = ref(null);
    const accept = ref(false);

    return {
      name,
      email,
      password,
      repeated_password,
      accept,

      onSubmit() {
        if (accept.value !== true) {
          $q.notify({
            color: "red-5",
            textColor: "white",
            icon: "warning",
            message: "You need to accept the license and terms first"
          });
        } else {
          var requestOptions = {
            method: "POST",
            redirect: "follow"
          };

          fetch(
            `http://stolowka.biz.dawisko.pl/api/register?name=${name.value}&email=${email.value}&password=${password.value}&terms=1`,
            requestOptions
          )
            .then(response => response.json())
            .then(result =>
              $q.notify({
                color: "green-4",
                textColor: "white",
                icon: "cloud_done",
                message: result.messages[0].message
              })
            )
            .catch(error =>
              $q.notify({
                color: "red-5",
                textColor: "white",
                icon: "warning",
                message: error.message
              })
            );
        }
      },

      onReset() {
        name.value = null;
        email.value = null;
        password.value = null;
        accept.value = false;
      }
    };
  }
};
</script>
