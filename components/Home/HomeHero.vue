<template>
  <section class="home-hero animated-block" ref="homeHero">
    <div class="home-hero__video-wrapper">
      <video
        class="video-wrapper__video"
        src="/images/Home/home-hero-video.webm"
        autoplay
        loop
        muted
        ref="heroVideoEl"
      ></video>
    </div>
    <div class="home-hero__copy">
      <p class="copy__body body">
        Welcome to Arcito - Crafting Architectural Masterpieces
      </p>
      <p class="copy__body body">
        At Arcito, we transcend the boundaries of conventional design to create
        architectural marvels that stand as timeless testaments to innovation
        and creativity.
      </p>
      <p class="copy__body body">
        ith a passion for precision and an unwavering commitment to excellence,
        we transform spaces into immersive experiences that inspire and
        captivate.
      </p>
    </div>
    <div class="home-hero__logo">
      <h2 class="logo__word">
        <span
          class="logo__char"
          v-for="(char, i) in logoSplitText"
          :key="char + i + 'home-hero'"
          >{{ char }}</span
        >
      </h2>
      <div class="honor__tag" id="photo">BEST IN Architecture</div>
      <div class="honor__tag">BUILDER'S CHOICE</div>
    </div>
  </section>
</template>

<script>
import { HomeHeroAnimations } from "~/animations/Home/HomeHero";
import { emitter as $eventBus } from "../../plugins/event-bus.js";

export default {
  inject: ["getTransitioned"],
  setup() {
    const homeHero = ref(null);
    const heroVideoEl = ref(null);

    function callback1() {
      HomeHeroAnimations.init(homeHero.value, false);
      heroVideoEl.value.play();
    }

    function callback2() {
      $eventBus.on("home-enter-animation", () => {
        HomeHeroAnimations.init(homeHero.value);
        heroVideoEl.value.play();
        $eventBus.off("home-enter-animation");
      });
    }

    useMuzenEnter(callback1, callback2);

    return {
      homeHero,
      heroVideoEl,
    };
  },
  computed: {
    logoSplitText() {
      return "Arcito".split("");
    },
  },
};
</script>

<style scoped>
@import url("~/styles/components/Home/HomeHero.pcss");
</style>
