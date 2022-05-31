<template>
    <form>
        <div class="card bg-dark">
            <div class="card-header text-center">
                <h1>Registrarse</h1>
            </div>
            <div class="card-body">
                <div class="form-group mb-2">
                    <label for="name" class="form-label">Nombre</label>
                    <input class="form-control" type="text" v-model="user.name">
                </div>
                <div class="form-group mb-2">
                    <label for="email">Correo electrónico</label>
                    <input class="form-control" type="text" v-model="user.email">
                </div>
                <div class="form-group mb-2">
                    <label for="password">Contraseña</label>
                    <input class="form-control" type="password" v-model="user.password">
                </div>
                <div class="form-group mb-2">
                    <label for="password_confirmation">Confirmar Contraseña</label>
                    <input class="form-control" type="password" v-model="user.password_confirmation">
                </div>
                <div class="form-group text-center">
                    <button type="button" class="btn btn-success" @click="register()">Registrarme</button>
                </div>
            </div>
        </div>
    </form>
</template>

<script>
    import axios from 'axios';
    export default {
        data() {
            return {
                user: {
                    name: '',
                    email: '',
                    password: '',
                    password_confirmation: ''
                }
            };
        },

        methods: {
            register() {
                console.log(this.user);
                axios.post('http://127.0.0.1:8000/api/register', this.user)
                    .then(({data}) => {
                        this.$router.push('/login');
                    })
                    .catch((error) => {
                        console.log(error);
                    });
            }
        }
    }
</script>