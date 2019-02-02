<template>
  <div class="hello">
    <h1 v-if="show">{{ msg }}</h1>

    <div v-for="(question, index) in quiz.questions" v-bind:key="question.id">
      <div v-show="index === questionIndex">
        <h4>{{ question.text }}</h4>
        <ol>
          <li v-for="response in question.responses" v-bind:key="response.id">
            <label>
              <input type="radio"
                     v-bind:value="response.choice"
                     v-bind:name="index"
                     v-model="picked"> {{ response.text }}
            </label>
          </li>
        </ol>

        <button v-on:click="check(question.correct, picked)">
          <span v-if="questionIndex == quiz.questions.length - 1">Finish</span>
          <span v-else>Next</span>
        </button>

        <h5>Benar: {{ totalCorrect }}</h5>
      </div>
    </div>

    <div v-show="questionIndex == quiz.questions.length">
      <h2>Kuis Selesai</h2>
      <p>Benar: {{ totalCorrect }} / {{ quiz.questions.length }}</p>
      <p>Nilai: {{ scoreCal() }}</p>
    </div>
  </div>
</template>

<script>
var quiz = {
  questions: [
    {
      text: "Siapakah James Potter itu ?",
      responses: [
        {text : 'Ayah Harry Potter', choice: 'A' },
        {text : 'Ibu Harry Potter', choice: 'B' },
        {text : 'Paman Harry Potter', choice: 'C' },
        {text : 'Kakek Harry Potter', choice: 'D' },
      ],
      correct : 'A'
    },
    {
      text: "Siapa Musuh Harry Sejak Kecil Hingga Dewasa ?",
      responses: [
        {text : 'Hermione Grangger', choice: 'A' },
        {text : 'Ron Weasley', choice: 'B' },
        {text : 'Luna Lovegood', choice: 'C' },
        {text : 'Draco Malfoy', choice: 'D' },
      ],
      correct : 'D'
    },
    {
      text: "Siapakah Penulis Buku Harry Potter ?",
      responses: [
        {text : 'Justin Timberlake', choice: 'A' },
        {text : 'J.K Rowlling', choice: 'B' },
        {text : 'Albert Einstein', choice: 'C' },
        {text : 'Bill Gates', choice: 'D' },
      ],
      correct : 'B'
    },
    {
      text: "Pilih Salah Satu Mantra Kutukan ?",
      responses: [
        {text : 'Wingardium Leviosa', choice: 'A' },
        {text : 'Riddiculus', choice: 'B' },
        {text : 'Avada Kedavra', choice: 'C' },
        {text : 'Obliviate', choice: 'D' },
      ],
      correct : 'C'
    },
    {
      text: "Hewan Peliharaan Harry Potter ?",
      responses: [
        {text : 'Burung Hantu', choice: 'A' },
        {text : 'Kucing', choice: 'B' },
        {text : 'Tikus', choice: 'C' },
        {text : 'Goblin', choice: 'D' },
      ],
      correct : 'A'
    },
  ]
};

export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: function() {
    return {
      picked: '',
      show: true,
      quiz: quiz,
      questionIndex: 0,
      totalCorrect: 0,
      userResponses: Array(quiz.questions.length).fill(false)
    }
  },
  methods: {
    check(correct, picked) {
      if (correct === picked) this.totalCorrect++;
      this.questionIndex++;
    },
    scoreCal: function() {
      return (100 / quiz.questions.length) * this.totalCorrect;
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
