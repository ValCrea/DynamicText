<script setup lang="ts">
import { computed } from "vue";

export interface Props {
  text: string;
  effect?: "sentence" | "word" | "letter";
  bounce?: string;
  delay?: number;
  offset?: number;
  animate?: boolean;
}

const props = withDefaults(defineProps<Props>(), {
  effect: "letter",
  bounce: "-100%",
  delay: 0,
  offset: 0.05,
  animate: true,
});

const words = computed(() => props.text.split(" "));
const sentence = computed(() => props.text.replace(/\s/g, "&nbsp;"));
</script>

<template>
  <div
    v-if="props.effect == 'sentence'"
    v-html="sentence"
    :class="{ 'text--animate': props.animate }"
    class="text"
  ></div>

  <div v-else class="text">
    <template v-if="props.effect == 'word'">
      <template v-for="(word, w) in words" :key="w">
        <div
          v-if="word"
          :style="{ 'animation-delay': `${props.delay + props.offset * w}s` }"
          :class="{ 'text--animate': props.animate }"
        >
          {{ word }}
        </div>
        <div v-if="w != words.length - 1">&nbsp;</div>
      </template>
    </template>

    <template v-else>
      <div v-for="(letter, l) in props.text" :key="l">
        <div
          v-if="letter != ' '"
          :style="{ 'animation-delay': `${props.delay + props.offset * l}s` }"
          :class="{ 'text--animate': props.animate }"
        >
          {{ letter }}
        </div>
        <div v-else>&nbsp;</div>
      </div>
    </template>
  </div>
</template>

<style scoped lang="scss">
.text {
  & * {
    display: inline-block;
  }

  &--animate {
    animation: bounce 0.5s infinite alternate ease-in-out;
    animation-delay: v-bind("`${props.delay}s`");
  }
}

@keyframes bounce {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(v-bind("props.bounce"));
  }
}
</style>
