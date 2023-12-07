<template>
    <div class="lesson__container">
        <h2 class="lesson__title">Step 1. Choose lessons</h2>
        <ul class="lesson__list">
            <li v-for="lesson in lessonsList" :key="lesson.id" class="lesson__item">
                <div v-if="lesson.teachersId.length" class="lesson__item">
                    <div class="lesson__name">{{ lesson.name }}</div>
                    <input v-model="selectedLessons" :value="lesson.id" type="checkbox" />
                </div>
            </li>
        </ul>
        <button class="lesson__button" @click="displaySelected">Choose the lesson</button>
        <div v-if="errorMessage" class="lesson__message">{{ errorMessage }}</div>
    </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
export default {
    name: 'LessonsSelectView',
    data() {
        return {
            selectedLessons: [],
        }
    },
    computed: {
        ...mapGetters('lessons', ['lessonsList']),
        ...mapGetters(['errorMessage']),
    },
    methods: {
        ...mapActions(['setErrorMessage']),
        displaySelected() {
            if (this.selectedLessons.length) {
                this.$router.push({
                    name: 'selected_lessons_list',
                    params: {
                        lessonId: this.selectedLessons,
                    },
                })
                this.setErrorMessage(null)
            } else {
                this.setErrorMessage('Будь ласка, виберіть принаймні один предмет')
            }
        },
    },
}
</script>

<style lang="scss" scoped>
.lesson {
    // .lesson__container

    &__container {
    }

    // .lesson__title

    &__title {
    }

    // .lesson__list

    &__list {
        display: flex;
        flex-direction: column;
        align-items: start;
        margin: 0 auto;
        gap: 15px;
        width: 300px;
    }

    // .lesson__item

    &__item {
        display: flex;
        justify-content: center;
        gap: 20px;
        margin-bottom: 5px;
    }

    // .lesson__name

    &__name {
    }

    // .lesson__button

    &__button {
    }

    // .lesson__message

    &__message {
    }
}
</style>
