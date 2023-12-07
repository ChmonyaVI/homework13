<template>
    <div class="login__container">
        <div class="login__block">
            <label>Login: <input v-model="userName" type="text" class="login__input" /></label>
            <label>Password: <input v-model="userPassword" type="text" class="login__input" /></label>
        </div>
        <button class="login__button" @click="userLogin">Login</button>
        <div v-if="errorMessage" class="login__message">{{ errorMessage }}</div>
    </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'
export default {
    name: 'LoginPage',
    data() {
        return {
            userName: null,
            userPassword: null,
        }
    },
    computed: {
        ...mapGetters(['errorMessage']),
    },
    methods: {
        ...mapActions(['setErrorMessage', 'setUserName']),
        userLogin() {
            this.setUserName(this.userName)

            if (this.userName && this.userPassword) {
                this.setErrorMessage(null)
                console.log(this.userName)

                if (this.$route.query.redirect) {
                    this.$router.push({
                        path: this.$route.query.redirect,
                    })
                } else this.$router.push({ name: 'home' })
            } else {
                this.setErrorMessage('Будь ласка, заповніть поля')
            }
        },
    },
}
</script>

<style lang="scss" scoped>
.login {
    // .login__container

    &__container {
    }

    // .login__block

    &__block {
        display: flex;
        flex-direction: column;
        gap: 20px;
    }

    // .login__input

    &__input {
    }
    // .login__input

    &__button {
        margin-top: 20px;
    }
    // .login__message
    &__message {
    }
}
</style>
