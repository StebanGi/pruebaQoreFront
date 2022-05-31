<template>
    <form id="login-form">
        <div class="card bg-dark">
            <div class="card-header">
                <h1 class="text-center">Iniciar sesión</h1>
            </div>
            <div class="card-body">
                <div class="mb-3">
                    <label for="email" class="form-control-label">Correo electrónico</label>
                    <input type="email" class="form-control" v-model="user.email">
                </div>
                <div class="mb-3">
                    <label for="password" class="form-control-label">Contraseña</label>
                    <input type="password" class="form-control" v-model="user.password">
                </div>
                <div class="form-group text-center">
                    <button type="button" @click="login" class="btn btn-success">Iniciar sesión</button>
                </div>
            </div>
        </div>
    </form>
</template>

<style>
</style>

<script>
  import Auth from '../Auth.js';
  import axios from 'axios';

    export default {
        data() {
            return {
                user: {
                    email: '',
                    password: '',
                }
            };
        },

        methods: {
            login() {
                axios.post('http://127.0.0.1:8000/api/login', this.user)
                    .then(({data}) => {
                        Auth.login(data.access_token,data.user);
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
