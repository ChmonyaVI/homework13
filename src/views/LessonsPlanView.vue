<template>
    <div class="lesson-plan__container">
        <h3 class="lesson-plan__title">Plans</h3>
        <div v-for="(assignment, index) in getFilledAssignmentsList" :key="assignment.id" class="lesson-plan__item">
            <div class="info">{{ assignment.lessonName }} -- {{ assignment.teacherName }}</div>
            <button type="button" class="lesson-plan__button" @click="deleteAssignment(index)">Delete</button>
        </div>
        <div v-if="getFilledAssignmentsList.length == 0" class="lesson-plan__message">List is Empty!</div>
    </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
export default {
    name: 'LessonsPlanView',
    computed: {
        ...mapGetters('assignments', ['getAssignmentsList', 'getFilledAssignmentsList']),
    },
    methods: {
        ...mapActions('assignments', ['deleteAssignment']),
    },
}
</script>

<style lang="scss" scoped>
.lesson-plan {
    // .lesson-plan__container

    &__container {
    }

    // .lesson-plan__title

    &__title {
    }

    // .lesson-plan__item

    &__item {
        display: flex;
        justify-content: start;
        display: flex;
        gap: 20px;
        align-items: center;
        width: 400px;
        margin: 0 auto;
        padding-top: 20px;
    }
}
.info {
}
.button {
}
</style>
