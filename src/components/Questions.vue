<template>
    <div class="questions-ctr">
        <div class="progress">
            <div class="bar" :style="{ width: `${questionsAnswered / questions.length * 100}%` }"></div>
            <div class="status">{{ questionsAnswered }} out of {{ questions.length }} questions answered</div>
        </div>
        <TransitionGroup name="fade"> <!-- enter-active-class="animate__animated animate_fadeIn"
            leave-active-class="animate__animated animate__fadeOut" -->
            <div class="single-question" v-for="(question, qIndex) in questions" :key="question.q"
                v-show="questionsAnswered === qIndex">
                <div class="question">{{ question.q }}</div>
                <div class="answers">
                    <div class="answer" v-for="answer in question.answers" @click.prevent="selectAnswer(answer.is_correct)">
                        {{ answer.text }}</div>
                </div>
            </div>
        </TransitionGroup>

    </div>
</template>

<script>
export default {
    props: ['questions',
        'questionsAnswered'
    ],
    emits: ["question-answered"],
    methods: {
        selectAnswer(is_correct) {
            this.$emit('question-answered', is_correct);
        },
    },

}
</script>

<style></style>