<template>
    <div>
        <div class="comp-question">
            <div class="comp-question__heading" @click="isShowAnswer=true" >
                {{Question}}
                <span v-if="isShowAnswer"> Real Answer: {{realAnswer}}</span>
            </div>
            <div class="comp-question__answers" :class="{'comp-question__answers_corners':!isWrong}">
                <div class="single-item">
                    <button class="btn-cls" :class="buttonType0" @click="checkAnswer(0)">{{answers[0]}}</button>
                </div>
                <div class="single-item">
                    <button class="btn-cls" :class="buttonType1" @click="checkAnswer(1)">{{answers[1]}}</button>
                </div>
                <div class="single-item">
                    <button class="btn-cls" :class="buttonType2" @click="checkAnswer(2)">{{answers[2]}}</button>
                </div>
                <div class="single-item">
                    <button class="btn-cls" :class="buttonType3" @click="checkAnswer(3)">{{answers[3]}}</button>
                </div>
            </div>
            <div class="comp-question__footer" v-if="isWrong">
                Wrong Answer. try again.
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
         switchFn: Function
    },
    data() {
        return {
            Question: '',
            firstNumber: 0,
            secondNumber: 0,
            realAnswer: 0,
            plusOrMinus: 0,
            answers: [0,0,0,0],
            isWrong: false,
            buttonType0:'btn-standard',
            buttonType1:'btn-standard',
            buttonType2:'btn-standard',
            buttonType3:'btn-standard',
            isShowAnswer: false
        }
    },
    created() {
            this.GenerateQuestion();
    },
    methods: {
        GenerateQuestion() {
            this.firstNumber = this.getRandomIntInclusive(1, 99);
            this.secondNumber =  this.getRandomIntInclusive(1, 99);
            this.plusOrMinus = this.getRandomIntInclusive(1, 2);

            this.Question = "What's " + this.firstNumber + (this.plusOrMinus == 1 ? ' + ' : ' - ' ) + this.secondNumber +"?";

            if(this.plusOrMinus == 1) {
                this.realAnswer = this.firstNumber +  this.secondNumber
            } else {
                this.realAnswer = this.firstNumber -  this.secondNumber;
            }

            for (let i=0; i<4; i++) {
                this.answers[i] = this.getRandomIntInclusive(-99, 99);
            }
            let x = this.getRandomIntInclusive(0, 3);
            this.answers[x] = this.realAnswer;
        },
        getRandomIntInclusive(min, max) {
            min = Math.ceil(min);
            max = Math.floor(max);
            return Math.floor(Math.random() * (max - min + 1)) + min;
             //The maximum is inclusive and the minimum is inclusive 
        },
        checkAnswer(index) {
            if (this.answers[index] == this.realAnswer )
            {
                this.switchFn();
            } else {
                switch(index) {
                    case 0:
                        this.buttonType0 = 'btn-no';
                        break;
                    case 1:
                        this.buttonType1 = 'btn-no';
                        break;
                    case 2:
                        this.buttonType2 = 'btn-no';
                        break;
                    case 3:
                        this.buttonType3 = 'btn-no';
                        break;
                }
                this.isWrong = true;
            }
        }

    }
    
}
</script>

<style scoped>

    .comp-question {
        width: 50%;
        margin: auto;
        border: 1px solid grey;
        border-radius: 6px;  
        max-width: 500px;
    }

    .comp-question__heading {
        background-color: lightgray;
        border-top-left-radius: 6px;
        border-top-right-radius: 6px;
        cursor: pointer;
    }

    .comp-question__heading:hover {
        background-color:#99ccff;
    }

    .comp-question__answers {
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-template-rows: 1fr 1fr;
        background-color:rgb(230, 240, 140);
    }

    .comp-question__answers_corners {
        border-bottom-left-radius: 6px;
        border-bottom-right-radius: 6px;
    }

    .single-item {
       margin-top: 10px;
       margin-bottom: 10px;  
    }

    .comp-question__footer {
        background-color:#ff3333;
        border-bottom-left-radius: 6px;
        border-bottom-right-radius: 6px;
    }



</style>



