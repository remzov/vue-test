<template>
    <div class="question">
        <div class="question__text">
            {{ question.text }}
        </div>
        <div class="uk-flex">
            <div v-for="variant in question.variants">
                <label>
                    {{ variant }}
                    <input type="radio" :name="question.id" :value="variant" v-on:click="$emit('answer', $event)">
                </label>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    props: ['question']
}

</script>

<style scoped>

.question {
    margin-bottom: 20px;
    padding: 20px;
    border: 1px solid #999;
}

.question__text {
    font-size: 30px;
}

label {
    margin-right: 25px;
    font-size: 24px;
}

</style>