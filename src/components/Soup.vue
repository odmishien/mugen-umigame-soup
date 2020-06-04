<template>
  <b-container fluid>
    <div v-if="!isStart">
      <b-form-group label="お題前半部分" label-for="first-half">
        <b-form-input id="first-half" v-model="firstHalf" placeholder="例:風が吹いた。"></b-form-input>
      </b-form-group>
      <b-form-group label="お題後半部分" label-for="second-half">
        <b-form-input id="second-half" v-model="secondHalf" placeholder="例:桶屋が儲かった。"></b-form-input>
      </b-form-group>
      <b-button @click="startGame" variant="success">ウミガメのスープを始める</b-button>
    </div>
    <div v-if="isStart">
      <div class="text-center">
        <h4>お題</h4>
        <h3>{{firstHalf}}</h3>
        <h3>{{secondHalf}}</h3>
      </div>

      <div class="my-5">
        <b-form inline>
          <b-col sm="1">
            <label for="question">質問:</label>
          </b-col>
          <b-col sm="9">
            <b-form-input
              id="question"
              class="w-100"
              placeholder="桶屋は桶を売ることで儲けることができた？"
              v-model="questionContent"
            ></b-form-input>
          </b-col>
          <b-col sm="2">
            <b-button @click="addQuestion(questionContent)" variant="danger">確かめる</b-button>
          </b-col>
        </b-form>
      </div>
      <div>
        <b-table hover :fields="tableFields" :items="questions">
          <template v-slot:cell(index)="data">{{data.index+1}}</template>
          <template v-slot:cell(answer)="data">{{data.item.answer ? 'YES' : 'NO'}}</template>
        </b-table>
      </div>
      <b-button @click="newGame" variant="success">新しいスープを始める</b-button>
    </div>
  </b-container>
</template>
<script>
export default {
  data() {
    return {
      isStart: false,
      firstHalf: "",
      secondHalf: "",
      questionContent: "",
      tableFields: [
        { key: "index", label: "No." },
        { key: "content", label: "質問" },
        { key: "answer", label: "答え" }
      ],
      questions: []
    };
  },
  methods: {
    startGame() {
      this.isStart = true;
    },
    addQuestion(content) {
      let answer = this.answerQuestion();
      this.questions.push({ content: content, answer: answer });
      this.questionContent = '';
    },
    answerQuestion() {
      return Math.random() >= 0.5;
    },
    newGame() {
      this.firstHalf = "";
      this.secondHalf = "";
      this.questionContent = "";
      this.questions.splice(-this.questions.length);
      this.isStart = false;
    }
  }
};
</script>
