<template>
    <div id="app">
        <div class="uk-container">
            <h1 class="uk-margin uk-text-center">Тест</h1>
            <div class="uk-margin">
                <question 
                    v-for="question in questions" 
                    :key="question.id" 
                    :question="question"
                    @answer="setAnswerArr($event)"
                >
                </question>
            </div>
            <button 
                class="uk-button uk-button-secondary uk-margin" 
                type="button" 
                @click="checkAnswers()" 
                :disabled="checked"
            >
                Проверить результат
            </button>
            <div 
                class="result" 
                v-show="checked == true"
            >
                {{ `${result} / ${this.questions.length}` }}
            </div>
        </div>
    </div>
</template>

<script>
import question from './question.vue';
export default {
    name: 'app',
    data () {
        return {
            questions: [
                {
                    id: 0,
                    text: 'Земля - плоская?',
                    variants: ['да', 'нет', 'она грязная!'],
                    answer: 'нет'
                },
                {
                    id: 1,
                    text: 'В Арктике холодно?',
                    variants: ['да', 'нет', 'где я?'],
                    answer: 'да'
                },
                {
                    id: 2,
                    text: 'Сколько будет 2 + 2?',
                    variants: ['4', 'я - гуманитарий!', 'нет'],
                    answer: '4'
                }
            ],
            answers: [],
            checked: false,
            result: 0
        }
    },
    methods: {
        setAnswerArr(event) {
            this.answers[event.target.name] = event.target.value;
        },
        checkAnswers() {
            for (let i = 0; i < this.questions.length; i++) {
                (this.questions[i].answer === this.answers[i]) ? this.result++ : this.result;
            }
            this.checked = true;
            document.querySelectorAll('input[type=radio]').forEach((input) => {
                input.disabled = true;
            });
        }
    },
    components: {
       'question': question
    },
}
 
</script>

<style scoped>
    
</style>
