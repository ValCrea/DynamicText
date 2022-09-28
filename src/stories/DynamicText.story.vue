<script setup lang="ts">
import DynamicText from "@/components/DynamicText.vue";
</script>

<template>
  <Story>
    <DynamicText
      text=" Hello  World and  Goodbye "
      type="slide"
      from="1rem"
      to="2rem"
      :duration="0.4"
      :offset="0.035"
    />
    <br />
    <DynamicText
      text=" Hello  World and  Goodbye "
      type="slide"
      from="1rem"
      to="2rem"
      :duration="0.4"
      :offset="-0.035"
    />
  </Story>
</template>
