<template>
    <div class="comp-correct">
        <div class="comp-correct_item">
            <div > 
                <div class="msg">That's Correct</div>
            </div>
            <hr>
            <div >
                <button class="btn-cls btn-standard" @click="CorrectAnswer">Next Question</button>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: {
         switchFn: Function
    },
    methods: {
        CorrectAnswer() {
            this.switchFn();
        }
    }
}
</script>

<style>
    .comp-correct {
        width: 50%;
        margin: auto;
        background-color: chartreuse;
        max-width: 500px;
    }

    .comp-correct_item {
        padding: 15px;
    }

    .msg {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        font-size:200%;
        text-align: center;
        color: green;
    }
</style>


