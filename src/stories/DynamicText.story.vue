<script setup lang="ts">
import { ref } from "vue";
import DynamicText from "@/components/DynamicText.vue";

const toggleWave = ref(false);
</script>

<template>
  <Story title="Dynamic Text" :layout="{ type: 'grid', width: '100%' }">
    <Variant title="Bounce sentence">
      <DynamicText
        class="test"
        text="This is a sentence"
        type="bounce"
        effect="sentence"
        to="-0.25rem"
        :duration="0.5"
        :offset="0.25"
      />
    </Variant>
    <Variant title="Bounce words">
      <DynamicText
        text="Sentences contain words"
        type="bounce"
        effect="word"
        to="-0.25rem"
        :duration="0.8"
        :offset="0.2"
      />
    </Variant>
    <Variant title="Bounce letters">
      <DynamicText
        text="Words contain letters"
        type="bounce"
        effect="letter"
        to="-0.25rem"
        :duration="0.5"
        :offset="0.1"
      />
    </Variant>
    <Variant title="Slide letters">
      <DynamicText
        text="Spin me please"
        type="slide"
        effect="letter"
        from="1rem"
        to="10rem"
        :duration="1.5"
        :offset="0.15"
      />
    </Variant>
    <Variant title="Slide letters reverse">
      <DynamicText
        text="Spin me  also "
        type="slide"
        effect="letter"
        from="1rem"
        to="10rem"
        :duration="1.5"
        :offset="-0.15"
      />
    </Variant>
    <Variant title="Color letter text">
      <DynamicText
        text="Red, blue and everything in between"
        type="color"
        effect="letter"
        from="red"
        to="blue"
        :duration="2"
        :offset="0.1"
        :delay="-20"
      />
    </Variant>
    <Variant title="Color word background">
      <DynamicText
        text="The background is nice but the code is nicer"
        type="background"
        effect="word"
        from="green"
        to="purple"
        :duration="3"
        :offset="-0.25"
      />
    </Variant>
    <Variant title="Letter Wave">
      <DynamicText
        text="~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~"
        type="bounce"
        effect="letter"
        to="-0.5rem"
        :duration="0.2"
        :offset="0.04"
        iteration="2"
        @click="toggleWave = !toggleWave"
        v-model:restart="toggleWave"
      />
    </Variant>
  </Story>
</template>
