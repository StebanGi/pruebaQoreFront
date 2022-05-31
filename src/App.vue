<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="d-flex justify-content-center">
      <div class="menu-btn-group">
        <div class="h2 text-white" v-if="Auth.user">Bienvenid@: {{Auth.user.name}}</div>
        <RouterLink class="btn btn-sm rounded-pill menu-btn" to="/login" v-if="!Auth.user">Iniciar sesión</RouterLink>
        <RouterLink class="btn btn-sm rounded-pill menu-btn" to="/register" v-if="!Auth.user">Registrarse</RouterLink>
        <button @click="logout()" class="btn btn-sm rounded-pill menu-btn" v-if="Auth.user">Cerrar sesión</button>
        <RouterLink class="btn btn-sm rounded-pill menu-btn" to="/edit-profile" v-if="Auth.user">Editar perfil</RouterLink>
        <RouterLink class="btn btn-sm rounded-pill menu-btn" to="/">Inicio</RouterLink>
      </div>
    </div>
  </header>

  <RouterView />
</template>

<script>
  import Auth from './Auth.js';
  import axios from 'axios'
  export default {
      data() {
          return {
              loggedUser: Auth.user
          };
      },
      mounted() {
          console.log(Auth.user);
      },
      methods: {
          logout() {
              axios.post('http://127.0.0.1:8000/api/logout')
              .then(({data}) => {
                  Auth.logout(); //reset local storage
                  this.$forceUpdate();
                  this.$router.push('/');
              })
              .catch((error) => {
                  console.log(error);
              });
          }
      }
  }
</script>

<style>
@import '@/assets/base.css';

#app {
  max-width: 1280px;
  margin: 0 auto;
  padding: 2rem;
  font-weight: normal;
}

header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

a,
.green {
  text-decoration: none;
  color: hsla(160, 100%, 37%, 1);
  transition: 0.4s;
}

@media (hover: hover) {
  a:hover {
    background-color: hsla(160, 100%, 37%, 0.2);
  }
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  body {
    display: flex;
    place-items: center;
  }

  #app {
    display: grid;
    grid-template-columns: 1fr 1fr;
    padding: 0 2rem;
    width: 100%;
  }

  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}

.menu-btn-group {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
.menu-btn {
  color: #FFF;
  background-color: gray;
  margin-top: 10px;
  font-weight: bold;
}
</style>
