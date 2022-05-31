<template>
    <form id="edit-profile-form">
        <div class="card bg-dark">
            <div class="card-header">
                <h1 class="text-center">Editar perfil</h1>
            </div>
            <div class="card-body">
                <div class="mb-3">
                    <label for="name" class="form-control-label">Nombre</label>
                    <input type="text" class="form-control" v-model="user.name">
                </div>
                <div class="form-group text-center">
                    <button type="button" @click="editProfile" class="btn btn-success">Cambiar nombre</button>
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
                    id: Auth.user.id,
                    name: Auth.user.name,
                }
            };
        },

        methods: {
            editProfile() {
                axios.post('http://127.0.0.1:8000/api/edit', this.user)
                    .then(({data}) => {
                        window.localStorage.setItem('user', JSON.stringify(data.user));
                        this.$router.push('/');
                    })
                    .catch((error) => {
                        console.log(error);
                    });
            }
        }
    }
</script>
