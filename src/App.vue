<template>
  <div id="app">
    <section class="hero is-primary">
      <div class="hero-body">
        <div class="container">
          <h1 class="title">Climate Change</h1>
        </div>
      </div>
    </section>
    <div class="columns is-mobile is-centered">
      <div class="column is-11">
        <div class="box">
          <div class="columns" v-if="end">
            <div class="column">
              <p>Correct: {{ correct }}%</p>
            </div>
          </div>
          <div class="columns" v-if="!end">
            <div class="column">
              <p>{{ questions[index].question }}</p>
            </div>
          </div>
          <div class="columns" v-if="!end">
            <div class="column">
              <div class="control">
                <label class="radio">
                  <input
                    type="radio"
                    name="answer"
                    :value="true"
                    v-model="picked"
                  />
                  True
                </label>
                <label class="radio">
                  <input
                    type="radio"
                    name="answer"
                    :value="false"
                    v-model="picked"
                  />
                  False
                </label>
              </div>
            </div>
          </div>
          <br />
          <div class="columns">
            <div class="buttons are-medium">
              <button
                @click="next"
                :disabled="picked === null"
                class="button is-primary"
                v-if="!end"
              >
                Next
              </button>
              <button @click="reset" class="button is-warning">Reset</button>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { questions } from './questions';

export default {
  name: 'app',
  data() {
    return {
      questions: questions,
      picked: null,
      index: 0,
      corrects: 0,
      end: false,
    };
  },
  methods: {
    next() {
      const a = this.questions[this.index];
      if (a.answer === this.picked) {
        this.corrects++;
      }

      if (this.index + 1 < this.questions.length) {
        this.index++;
        this.picked = null;
      } else {
        this.end = true;
      }
    },
    reset() {
      this.index = 0;
      this.corrects = 0;
      this.end = false;
      this.picked = null;
    },
  },
  computed: {
    correct() {
      return ((this.corrects * 100) / this.questions.length).toFixed(2);
    },
  },
};
</script>

<style lang="sass" src="bulma"></style>
<style>
.box {
  margin-top: 24px;
}
#app {
  margin: 0;
}
</style>
