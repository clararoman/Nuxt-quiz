<template>
  <div class="quiz-wrapper">
    <div class="row" v-if="status=='ongoing'">
      <h2 class="col-12 score">Your score: {{score}}</h2>
      <div class="col-12 question" v-html="currentItem.question"></div>
      <div
        class="option-wrapper col-6"
        v-for="(option, i) in allOptions"
        :key="i"
        @click="checkAnswer"
        :value="option"
        ref="option"
      >
        <b-button variant="info" v-html="option" class="btn w-100" :class="'btn-'+i"></b-button>
      </div>
      <div class="controls col-12">
        <nuxt-link to="/quiz">
          <b-button class="exit-btn col-2" variant="outline-danger" pill>Exit</b-button>
        </nuxt-link>
        <b-button class="skip-btn col-2" variant="dark" pill @click="nextItem()">Skip</b-button>
      </div>
    </div>
    <div class="row" v-else-if="status=='completed'">
      <h2 class="col-12">Your final score is {{score}} out of 20</h2>
      <h4 class="col-12">{{message}}</h4>
      <div class="col-12">
        <b-button @click="startQuiz()">Try again</b-button>
        <nuxt-link to="/quiz">
          <b-button>Change category</b-button>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";
import axios from "axios";

export default {
  data() {
    return {
      id: this.$route.params.id,
      score: 0,
      currentIndex: 0,
      status: "ongoing"
    };
  },
  async asyncData({ params }) {
    const quiz = await axios.get(
      `https://opentdb.com/api.php?amount=20&category=${params.id}`
    );
    return {
      quiz: quiz.data.results
    };
  },
  computed: {
    ...mapState(["list"]),
    category() {
      return this.list.find(el => el.id === this.id);
    },
    message() {
      if (this.score < 11) {
        return "Better luck next time.";
      } else {
        return "A person of culture, i see. Good job.";
      }
    },
    currentItem() {
      return this.quiz[this.currentIndex];
    },
    allOptions() {
      let options = [];
      let incorrect = this.currentItem.incorrect_answers;
      let correct = this.currentItem.correct_answer;

      incorrect.forEach(element => {
        options.push(element);
      });
      options.push(correct);
      return this.shuffle(options);
    }
  },
  methods: {
    startQuiz() {
      this.score = 0;
      this.status = "ongoing";
      this.currentIndex = 0;
    },
    checkAnswer: function(event) {
      event.target.classList.remove("btn-info");
      if (event.target.innerHTML == this.currentItem.correct_answer) {
        this.score++;
        event.target.classList.add("btn-success");
      } else {
        event.target.classList.add("btn-danger");
        this.$refs.option.forEach(element => {
          if (
            element.children[0].innerHTML == this.currentItem.correct_answer
          ) {
            element.children[0].classList.remove("btn-info");
            element.children[0].classList.add("btn-success");
          }
        });
      }

      setTimeout(this.nextItem, 1000);
    },
    nextItem() {
      this.$refs.option.forEach(element => {
        element.children[0].blur();
        element.children[0].classList.remove("btn-success", "btn-danger");
        element.children[0].classList.add("btn-info");
        console.log(element.children);
      });
      if (this.currentIndex == 19) {
        this.status = "completed";
      } else {
        this.currentIndex++;
      }
    },
    shuffle(array) {
      var currentIndex = array.length,
        temporaryValue,
        randomIndex;

      while (0 !== currentIndex) {
        randomIndex = Math.floor(Math.random() * currentIndex);
        currentIndex -= 1;

        // And swap it with the current element.
        temporaryValue = array[currentIndex];
        array[currentIndex] = array[randomIndex];
        array[randomIndex] = temporaryValue;
      }

      return array;
    }
  }
};
</script>

<style lang="scss">
.quiz-wrapper {
  .option-wrapper > div {
    background-color: #262626;
    color: white;
  }
  .controls {
    position: relative;
    margin-top: 2rem;
    padding: 1rem;
    .skip-btn {
      float: right;
      margin-left: 2rem;
    }
    .exit-btn {
      position: absolute;
      bottom: 1rem;
      left: 1rem;
    }
  }
}
</style>