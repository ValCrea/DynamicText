<script setup lang="ts">
import { computed } from "vue";

export interface Props {
  text: string;

  type?: "bounce" | "slide" | "none";
  effect?: "sentence" | "word" | "letter";
  from?: string;
  to?: string;
  offset?: number;
  animate?: boolean;

  delay?: number;
  duration?: number;
  iteration?: string;
  direction?: string;
  timing?: string;
}

const props = withDefaults(defineProps<Props>(), {
  type: "none",
  effect: "letter",
  from: "",
  to: "",
  offset: 0.01,
  animate: true,

  delay: 0,
  duration: 1,
  iteration: "infinite",
  direction: "alternate",
  timing: "ease-in-out",
});

const animationClass = computed(() => {
  if (props.type === "bounce") return "text--bounce";
  if (props.type === "slide") return "text--slide";
  return "";
});

const words = computed(() => props.text.split(" "));
const sentence = computed(() => props.text.replace(/\s/g, "&nbsp;"));
</script>

<template>
  <div
    v-if="props.effect == 'sentence'"
    v-html="sentence"
    :class="[{ 'text--animate': props.animate }, animationClass]"
    class="text"
  ></div>

  <div v-else class="text">
    <template v-if="props.effect == 'word'">
      <template v-for="(word, w) in words" :key="w">
        <div
          v-if="word"
          :style="{ 'animation-delay': `${props.delay + props.offset * w}s` }"
          :class="[{ 'text--animate': props.animate }, animationClass]"
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
          :class="[{ 'text--animate': props.animate }, animationClass]"
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
  display: inline-block;

  & * {
    display: inline-block;
  }

  &--animate {
    animation-duration: v-bind("`${props.duration}s`");
    animation-iteration-count: v-bind("props.iteration");
    animation-direction: v-bind("props.direction");
    animation-timing-function: v-bind("props.timing");
    animation-delay: v-bind("`${props.delay}s`");
  }

  &--bounce {
    animation-name: bounce;
  }
  &--slide {
    animation-name: slide;
  }
}

@keyframes bounce {
  from {
    transform: translateY(v-bind("props.from"));
  }
  to {
    transform: translateY(v-bind("props.to"));
  }
}

@keyframes slide {
  from {
    transform: translateX(v-bind("props.from"));
  }
  to {
    transform: translateX(v-bind("props.to"));
  }
}
</style>
