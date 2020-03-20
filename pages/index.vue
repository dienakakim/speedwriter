<template>
  <div class="bg-gray-900 w-screen h-screen px-12 py-6 flex flex-col overflow-hidden">
    <Logo
      class="text-2xl sm:text-4xl lg:text-6xl text-white text-center"
      :title="title"
    />
    <div class="py-6">
      <hr>
    </div>
    <div
      class="flex flex-col justify-center items-center"
      :class="{ hidden: timerStarted }"
    >
      <div class="text-lg sm:text-2xl lg:text-4xl justify-center text-center text-gray-200">
        Welcome! This is a speedwriting tool that interprets Markdown.
      </div>
      <button
        class="border-4 rounded-lg text-gray-200 text-xl py-2 px-4 mt-4 hover:cursor-pointer hover:bg-gray-700"
        @click.once="startTimer(COUNTDOWN_TIMER)"
      >
        Start
      </button>
    </div>
    <div
      class="flex flex-col justify-center items-center"
      :class="{ hidden: !timerEnded }"
    >
      <div class="text-2xl justify-center text-center text-gray-200">
        Time's up! Here's what you wrote:
      </div>
    </div>
    <div
      class="flex flex-col flex-1"
      :class="{ hidden: !timerStarted }"
    >
      <div class="flex flex-1 max-h-screen py-4">
        <div class="flex-1">
          <!-- Typing area -->
          <textarea
            name="Typing area"
            id="typing-area"
            class="text-md sm:text-xl lg:text-2xl text-gray-200 font-mono w-full h-full resize-none rounded-lg p-4"
            v-model="
            content"
            @click.once="emptyContent"
            :readonly="timerEnded"
            :class="{ 'bg-black': !timerEnded, 'bg-transparent': timerEnded }"
          ></textarea>
        </div>
        <div class="flex justify-center px-4">
          <!-- Vertical bar -->
          <div class="border-l-2">
          </div>
        </div>
        <div class="flex-1 flex">
          <!-- Markdown Preview -->
          <MarkdownPreview
            class="text-gray-200 text-md sm:text-xl lg:text-2xl overflow-auto w-full h-full bg-transparent rounded-lg p-4"
            :text="content"
            :class="{ 'bg-transparent': !timerEnded, 'bg-black': timerEnded }"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/logo/Logo';
import MarkdownPreview from '~/components/mdpreview/MarkdownPreview';
import moment from 'moment';
const COUNTDOWN_TIMER = process.env.COUNTDOWN_TIMER;
export default {
  name: 'index',
  components: {
    Logo,
    MarkdownPreview
  },
  data() {
    return {
      timerStarted: false,
      timerEnded: false,
      content: 'Type your text here!',
      timer: 0,
      anyContentTyped: false,
      COUNTDOWN_TIMER
    };
  },
  methods: {
    decrementTimer(timeout) {
      --this.$data.timer;
      if (this.$data.timer !== 0) {
        setTimeout(this.decrementTimer, 1000);
      } else {
        this.$data.timerEnded = true;
        if (!this.$data.anyContentTyped) {
          this.$data.content = "You haven't written anything 😢";
        }
      }
    },
    startTimer(time) {
      this.$data.timer = time;
      this.$data.timerStarted = true;
      setTimeout(this.decrementTimer, 1000);
    },
    emptyContent() {
      if (!this.$data.timerEnded) {
        this.$data.content = '';
        this.$data.anyContentTyped = true;
      }
    }
  },
  computed: {
    title() {
      return this.$data.timerStarted ? this.timeView : 'SpeedWriter';
    },
    timeView() {
      return moment(0, 'HH')
        .seconds(this.$data.timer)
        .format('m:ss');
    },
  }
};
</script>

<style>
</style>
