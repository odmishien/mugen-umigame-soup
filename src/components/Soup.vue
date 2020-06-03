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
      <Question />
    </div>
  </b-container>
</template>
<script>
import Question from "./Question";
export default {
  components: {
    Question
  },
  data() {
    return {
      isStart: false,
      firstHalf: "",
      secondHalf: ""
    };
  },
  methods: {
    startGame() {
      this.isStart = true;
    }
  }
};
</script>
