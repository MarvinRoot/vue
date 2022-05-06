<template>
    <form class="review-form" @submit.prevent="onSubmit">
        <h3>Leave a review</h3>
        <label for="name">Name:</label>
        <input id="name" v-model="name" required>
        
        <label for="review">Review:</label>
        <textarea id="review" v-model="review" required></textarea>

        <label for="rating">Rating:</label>
        <select id="rating" v-model.number="rating" required>
            <option>5</option>
            <option>4</option>
            <option>3</option>
            <option>2</option>
            <option>1</option>
        </select>

        <input class="button" type="submit" value="Submit">

    </form>
</template>

<script>
import { ref } from 'vue'

export default {
    data() {
        return {
            name: '',
            review: '',
            rating: null,
            cussWords: ['skandal', 'tmerr']
        }
    },
    methods: {
        onSubmit(){

            let productReview = {
                name: this.name,
                review: this.review,
                rating: this.rating
            }

            this.$emit('review-submitted', productReview)

        }   
    }
}
</script>

<style scoped>
input[type='text'] {
    padding: 5px;
}

button {
    margin-top: 20px;
}
</style>