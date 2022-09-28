<script setup lang="ts">
import { ref, computed, watch } from "vue";

export interface Props {
  text: string;

  type?: "bounce" | "slide" | "color" | "background" | "none";
  effect?: "sentence" | "word" | "letter";
  from?: string;
  to?: string;
  offset?: number;

  delay?: number;
  duration?: number;
  iteration?: string;
  direction?: string;
  timing?: string;

  restart?: any;
}
const props = withDefaults(defineProps<Props>(), {
  type: "none",
  effect: "letter",
  from: "",
  to: "",
  offset: 0.01,

  delay: 0,
  duration: 1,
  iteration: "infinite",
  direction: "alternate",
  timing: "ease-in-out",

  restart: null,
});

const animations = ref();
watch(
  () => props.restart,
  () => {
    animations.value.forEach((element: HTMLElement) => {
      element.style.animation = "none";
      element.offsetHeight; /* trigger reflow */
      element.style.animation = "";
    });
  }
);

const animationClass = computed(() => {
  if (props.type === "bounce") return "animate--bounce";
  if (props.type === "slide") return "animate--slide";
  if (props.type === "color") return "animate--color";
  if (props.type === "background") return "animate--background";
  return "";
});

const words = computed(() => props.text.split(" "));
const sentence = computed(() => props.text.replace(/\s/g, "&nbsp;"));
</script>

<template>
  <div class="text">
    <template v-if="props.effect === 'sentence'">
      <div
        v-html="sentence"
        :class="['animate', animationClass]"
        :ref="(el) => (animations = [el])"
        aria-hidden="true"
      ></div>
    </template>

    <template v-else-if="props.effect === 'word'">
      <div
        v-for="(word, w) in words"
        :key="w"
        :style="{ 'animation-delay': `${props.delay + props.offset * w}s` }"
        :class="['animate', animationClass]"
        ref="animations"
        aria-hidden="true"
      >
        {{ word }}
        <template v-if="w != words.length - 1">&nbsp;</template>
      </div>
    </template>

    <template v-else>
      <div
        v-for="(letter, l) in props.text"
        :key="l"
        :style="{ 'animation-delay': `${props.delay + props.offset * l}s` }"
        :class="['animate', animationClass]"
        ref="animations"
        aria-hidden="true"
      >
        <template v-if="/\s/.test(letter)">&nbsp;</template>
        <template v-else>{{ letter }}</template>
      </div>
    </template>

    <div aria-label="{{props.text}}" />
  </div>
</template>

<style scoped lang="scss">
.text {
  display: inline-block;

  & * {
    display: inline-block;
  }
}

.animate {
  animation-duration: v-bind("`${props.duration}s`");
  animation-iteration-count: v-bind("props.iteration");
  animation-direction: v-bind("props.direction");
  animation-timing-function: v-bind("props.timing");
  animation-delay: v-bind("`${props.delay}s`");

  &--bounce {
    animation-name: bounce;
  }
  &--slide {
    animation-name: slide;
  }
  &--color {
    animation-name: color;
  }
  &--background {
    animation-name: background;
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

@keyframes color {
  from {
    color: v-bind("props.from");
  }
  to {
    color: v-bind("props.to");
  }
}

@keyframes background {
  from {
    background-color: v-bind("props.from");
  }
  to {
    background-color: v-bind("props.to");
  }
}
</style>
