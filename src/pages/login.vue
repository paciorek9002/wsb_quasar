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
        v-model="password"
        label="Your Password *"
        type="password"
        lazy-rules
        :rules="[
          val => (val && val.length > 8) || 'Provide long enough password'
        ]"
      />

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
    const password = ref(null);

    return {
      name,
      password,

      onSubmit() {
           $q.notify({
            color: "red-5",
            textColor: "white",
            icon: "warning",
            message: "Masno Jest"
          });
      },

      onReset() {
        name.value = null;
        password.value = null
      }
    };
  }
};
</script>
