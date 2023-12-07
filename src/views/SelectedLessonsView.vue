<template>
    <div class="lesson-content__container">
        <h2 class="lesson-content__title">Step 2: Choose teachers</h2>
        <ul class="lesson-content__list">
            <li v-for="lessonId in selectedLessonsList" :key="lessonId" class="lesson-content__item">
                <h4 class="lesson-content__name">{{ getLessonById(lessonId).name }}</h4>
                <div class="lesson-content__selected-item">
                    <label>
                        <select v-model="getLessonById(lessonId).selectedTeacher">
                            <option
                                v-for="teacherName in getLessonById(lessonId).teachersId"
                                :key="teacherName"
                                :value="teacherName"
                            >
                                {{ getTeacherById(teacherName).name }}
                            </option>
                        </select>
                    </label>
                </div>
            </li>
        </ul>
        <button class="button" @click="addNewAssignment">Get started</button>
        <div v-if="errorMessage" class="err-msg">{{ errorMessage }}</div>
    </div>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'
export default {
    name: 'SelectedLessonsView',
    data() {
        return {
            selectTeacher: null,
        }
    },
    computed: {
        ...mapGetters('lessons', ['getLessonById', 'getFilledSelectedList']),
        ...mapGetters('teachers', ['getTeacherById', 'teachersList']),
        ...mapGetters(['errorMessage']),
        selectedLessonsList() {
            return this.$route.params.lessonId
        },
    },
    methods: {
        ...mapActions('assignments', ['addAssignment']),
        ...mapActions(['setErrorMessage']),
        addNewAssignment() {
            const assignmentsToAdd = this.selectedLessonsList.map((lessonId) => ({
                lessonId,
                teacherId: this.getLessonById(lessonId).selectedTeacher,
            }))
            assignmentsToAdd.forEach((assignment) => {
                if (assignment.teacherId) {
                    this.setErrorMessage(null)
                    this.addAssignment(assignment)
                    this.$router.push({
                        name: 'lessons_list',
                        params: {
                            lessonId: this.selectedLessonsList,
                            teacherId: this.getLessonById(this.selectedLessonsList[0]).selectedTeacher,
                        },
                    })
                } else this.setErrorMessage('Будь ласка, виберіть вчителів')
                console.log(assignment.teacherId)
            })
        },
    },
}
</script>

<style lang="scss" scoped>
.lesson-content {
    // .lesson-content__container

    &__container {
    }

    // .lesson-content__title

    &__title {
    }

    // .lesson-content__list

    &__list {
    }

    // .lesson-content__item

    &__item {
        display: flex;
        align-items: center;
        gap: 20px;
        justify-content: center;
    }

    // .lesson-content__name

    &__name {
    }

    // .lesson-content__selected-item

    &__selected-item {
    }
}
.button {
}
.err-msg {
}
</style>
