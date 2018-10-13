<template>
  <div id="app">
    <h1><strong>The Super Quiz</strong></h1>
    <hr>
    <transition name="flip"
                mode="out-in">
        <component :is="selectedComponent" :switchFn="switchComponents"></component>
    </transition>
  </div>
</template>

<script>
import Question from './components/Question.vue';
import Correct from './components/Correct.vue';

export default {
  name: 'app',
  data () {
    return {
      selectedComponent: 'app-question'
    }
  },
  components: {
    appQuestion: Question,
    appCorrect: Correct
  },
  methods: {
    created: function() {
       console.log('!!!!!!Parent Created!!!!!!');
       GenerateQuestion();  
    },
    switchComponents() {
      this.selectedComponent == 'app-question' ?  this.selectedComponent = 'app-correct' :  this.selectedComponent = 'app-question';
    }
  }

}
</script>

<style >
* {
  box-sizing: border-box;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  font-size: large;
  text-align: center;
}

h1, h2 {
  font-weight: normal;
}

.flip-enter-active {
    animation: flip-in 0.5s ease-out forwards;
}

.flip-leave-active {
    animation: flip-out 0.5s ease-out forwards;
}

@keyframes flip-out {
  from {
      transform: rotateY(0deg);
  }
  to {
      transform: rotateY(90deg);
  }
}

@keyframes flip-in {
  from {
    transform: rotateY(90deg);
  }
  to {
    transform: rotateY(0deg);
  }
}


.btn-cls {
    padding: 6px 12px;
    margin-bottom: 0;
    font-size: 14px;
    font-weight: 400;
    line-height: 1.42857143;
    text-align: center;
    white-space: nowrap;
    vertical-align: middle;
    touch-action: manipulation;
    cursor: pointer;
    border: 1px solid transparent;
    border-radius: 4px;
    color: #fff;
    min-width: 47px;
    text-decoration: none;
}

.btn-standard {
    color: #fff;
    background-color: #337ab7;
    border-color: #2e6da4;
}

.btn-standard:hover,
.btn-standard:active,
.btn-standard:focus,
.btn-standard:focus-within {
    color: #fff;
    background-color: #2b6495;
    border-color: #2e6da4;
    text-decoration: none;
}

.btn-no {
    color: #fff;
    background-color: #d9534f;
    border-color: #d43f3a;
}

</style>
