<template>
<link rel="preconnect" href="https://fonts.googleapis.com">
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
    <link href="https://fonts.googleapis.com/css2?family=Do+Hyeon&display=swap" rel="stylesheet">
    <div id="app">
         <nav class="navbar navbar-expand  navbar-dark bg-primary">
            <a href="/" classv class="navbar navbar-expand  navbar-dark bg-primary"></a>
            <a href="/" class="navbar-brand"><img id="sme" src="./assets/sme.png"></a>
            <div class="navbar-nav mr-auto">
                <li class="nav-item">
                    <router-link to="/home" class="nav-link">
                        <font-awesome-icon icon="home"/>
                        Home
                    </router-link>
                </li>
                <li v-if="showAdminBoard" class="nav-item">
                    <router-link to="/admin" class="nav-link">Admin Board</router-link>
                </li>
                <li v-if="showModeratorBoard" class="nav-item">
                    <router-link to="/mod" class="nav-link">Moderator Board</router-link>
                </li>
                <li class="nav-item">
                    <router-link v-if="currentUser" to="/user" class="nav-link">User</router-link>
                </li>
            </div>
            <div v-if="!currentUser" class="navbar-nav ml-auto">
                <li class="nav-item">
                    <router-link to="/register" class="nav-link">
                        <font-awesome-icon icon="user-plus"/>
                        Sign Up
                    </router-link>
                </li>
                <li class="nav-item">
                    <router-link to="/login" class="nav-link">
                        <font-awesome-icon icon="sign-in-alt"/>
                        Login
                    </router-link>
                </li>
            </div>
            <div v-if="currentUser" class="navbar-nav ml-auto">
                <li class="nav-item">
                    <router-link to="/profile" class="nav-link">
                        <font-awesome-icon icon="user"/>
                        {{ currentUser.username }}
                    </router-link>
                </li>
                <li class="nav-item">
                    <a class="nav-link" @click.prevent="logOut">
                        <font-awesome-icon icon="sign-out-alt"/>
                        LogOut
                    </a>
                </li>
            </div>
        </nav>
        <div class="container">
            <router-view/>
        </div>
    </div>
</template>
<script>
    export default {
        computed: {
            currentUser() {
                return this.$store.state.auth.user;
            },
            showAdminBoard() {
                if (this.currentUser && this.currentUser['roles']) {
                    return this
                        .currentUser['roles']
                        .includes('ROLE_ADMIN');
                }
                return false;
            },
            showModeratorBoard() {
                if (this.currentUser && this.currentUser['roles']) {
                    return this
                        .currentUser['roles']
                        .includes('ROLE_MODERATOR');
                }
                return false;
            }
        },
        methods: {
            logOut() {
                this
                    .$store
                    .dispatch('auth/logout');
                this
                    .$router
                    .push('/login');
            }
        }
    };
</script>

<style scoped>
@import url(//fonts.googleapis.com/earlyaccess/nanumpenscript.css);

#sme {
    width:59px;
    height:63px;
    top:1px
}

template { background: #2980B9;  
    background: -webkit-linear-gradient(to top, #FFFFFF, #d3f3ff, rgb(158, 216, 255)); 
    background: linear-gradient(to top, #FFFFFF, #d3f3ff, rgb(158, 216, 255));     
}

.container{
    position: relative;
    top:40px;
}

.navbar-brand{
    font-family: 'Do Hyeon', sans-serif;
    font-size: 24px;
}

.navbar-expand  navbar-dark bg-primary {
    height:50px;
}

nav {
    height: 63px;
}
</style>