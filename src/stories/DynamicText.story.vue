<script setup lang="ts">
import DynamicText from "@/components/DynamicText.vue";
</script>

<template>
  <Story title="Dynamic Text" :layout="{ type: 'grid', width: '100%' }">
    <Variant title="Bounce sentence">
      <DynamicText
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
        :duration="0.6"
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
        text="H e l l o   W o r l d"
        type="slide"
        effect="letter"
        from="1rem"
        to="10rem"
        :duration="2"
        :offset="0.1"
      />
    </Variant>
    <Variant title="Slide letters reverse">
      <DynamicText
        text="H e l l o   W o r l d"
        type="slide"
        effect="letter"
        from="1rem"
        to="10rem"
        :duration="2"
        :offset="-0.1"
      />
    </Variant>
  </Story>
</template>
