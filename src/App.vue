<template>
    <nav class="test">
        <router-link :to="{ name: 'home' }">Home</router-link> |
        <router-link :to="{ name: 'login' }">Login</router-link> |
        <router-link v-if="userName" :to="{ name: 'select_lessons' }">Lessons</router-link>
        <div class="login__block">
            <h5 class="login__title">{{ userName }}</h5>
            <button class="login__button" @click="onAction">{{ buttonLoginTitle }}</button>
        </div>
    </nav>
    <router-view />
</template>
<script>
import { mapGetters, mapActions } from 'vuex'
export default {
    computed: {
        ...mapGetters(['userName']),
        buttonLoginTitle() {
            return this.userName ? 'Вихід' : 'Вхід'
        },
    },
    methods: {
        ...mapActions(['setUserName']),
        onAction() {
            if (!this.userName) {
                this.$router.push({
                    name: 'login',
                })
            } else {
                this.setUserName(null)
                this.$router.push({
                    name: 'home',
                })
            }
        },
    },
}
</script>

<style lang="scss">
.test {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
}
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

nav {
    padding: 30px;

    a {
        font-weight: bold;
        color: #2c3e50;

        &.router-link-exact-active {
            color: #42b983;
        }
    }
}
.login {
    // .login__block

    &__block {
        display: flex;
        align-items: center;
        gap: 20px;
    }

    // .login__title

    &__title {
        color: black;
    }

    // .login__button

    &__button {
    }
}
</style>
