<template>
  <q-page class="flex flex-center">
    <q-list dense bordered padding class="rounded-borders">
      <q-item clickable v-ripple v-for="item in items" :key="item.text">
        <q-item-section>{{item.text}}</q-item-section>
      </q-item>
    </q-list>
  </q-page>
</template>

<script>
import { defineComponent } from "vue";

const items = [
  {
    text: "jakiś tekst",
    link: "link"
  },
  {
    text: "jakiś tekst",
    link: "link"
  },
  {
    text: "jakiś tekst",
    link: "link"
  }
];

export default defineComponent({
  name: "PageIndex",
  setup() {
    return {
      items: items
    };
  }
});
</script>
