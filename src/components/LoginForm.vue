<template>
    <div  id="login-container" >
        <h1 class="login title">Login</h1>
        <form @submit.prevent="login()" id="login-form">
            <label class="email-label login" for="email">Email:</label><br>
            <input v-model="email" class="email-input login" type="text" id="email-login" name="email" ><br>
            <label class="password-label login" for="password">Password:</label><br>
            <input v-model="password" class="password-input login" type="password" id="password-login" name="password"><br><br>
            <input class="submit" type="submit" value="Login">
            <a id="register-word" @click="changePage('registerDisplay')">Doesn't have an account yet? Register here</a>
        </form>
        <div id="my-signin2"></div>
    </div>
</template>

<script>
export default {
    data: function () {
        return {
            email: '',
            password: '',
            currentPage: '',            
        }
    },
    methods: {
        login: function () {
            let obj = {
                email: this.email,
                password: this.password
            }
            this.$emit('loginObj', obj)
        },
        changePage: function (inputPage) {
            this.currentPage = inputPage
            this.$emit('curPage', this.currentPage)
        },
        onSignIn: function (googleUser){
            this.$emit('onSignIn', googleUser)
        },
        onFailure: function(error) {
            console.log(error);
        }
    },
    mounted() {
        // function renderButton() {
                gapi.signin2.render('my-signin2', {
                    'scope': 'profile email',
                    'width': 240,
                    'height': 50,
                    'longtitle': true,
                    'theme': 'dark',
                    'onsuccess': this.onSignIn,
                    'onfailure': this.onFailure
                });
            // }
    }
}
</script>

<style>

</style>