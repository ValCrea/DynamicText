<script setup lang="ts">
import { ref } from "vue";
import DTextBounce from "@/components/DTextBounce.vue";

const animate = ref(true);
</script>

<template>
  <Story>
    <br />
    <button @click="animate = !animate">Animate</button>
    <br />
    <DTextBounce text="He ll  o " :delay="1" :animate="animate" />
    <DTextBounce text="He ll  o " effect="word" :delay="2" :animate="animate" />
    <DTextBounce
      text="He ll  o "
      effect="sentence"
      :delay="3"
      :animate="animate"
    />
  </Story>
</template>
