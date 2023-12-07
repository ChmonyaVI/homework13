<template>
    <div class="home">
        <h1 v-if="userName">Welcome, {{ userName }}, to our sites!</h1>
        <h2 v-if="!userName">Welcome, to our sites!</h2>
        <h5 v-if="!userName">Please log in.</h5>
    </div>
</template>

<script>
import { mapGetters } from 'vuex'
// @ is an alias to /src

export default {
    name: 'HomeView',
    components: {},
    computed: {
        ...mapGetters(['userName']),
    },
}
</script>
