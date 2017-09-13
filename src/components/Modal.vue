<template>
    <div class="modal">
      <div class="modal-background" @click="$emit('closeModal')"></div>
      <div class="modal-card">
        <header class="modal-card-head">
          <p class="modal-card-title">Information about the user</p>
          <button class="delete" aria-label="close" @click="$emit('closeModal')"></button>
        </header>
        <section class="modal-card-body" v-if="!user">
          <div class="loader" v-if="activeLoader"></div>
          <div v-if="!activeLoader">
            <p>There are no user with this nickname</p>
          </div>
        </section>
        <section class="modal-card-body" v-else>
          <div class="loader" v-if="activeLoader"></div>
          <div v-if="!activeLoader">
            <figure class="user-image image is-128x128">
              <img :src="user.avatar_url" :alt="user.login" class="is-center">
            </figure>
            <a :href="user.html_url"><h2>{{ user.login }}</h2></a>
            <small>{{ user.bio }}</small>
          </div>
        </section>
      </div>
    </div>
</template>

<script>
    import axios from 'axios';

    export default {
        data() {
          return {
            user: {},
            activeLoader: true,
          }
        },
        props: [
            'nickname'
        ],
        created() {
          axios.get(`https://api.github.com/users/${this.nickname}`)
            .then(response => {
              this.user = response.data;
            })
            .catch(error => {
              this.user = false;
            })
        },
        mounted() {
          setTimeout(() => {
            this.activeLoader = false;
          }, 1000);
        },
    }
</script>

<style>
  .modal-card-body {
    text-align: center;
  }
  .loader {
      border: 16px solid #f3f3f3; /* Light grey */
      border-top: 16px solid #3498db; /* Blue */
      border-radius: 50%;
      width: 120px;
      height: 120px;
      animation: spin 2s linear infinite;
      margin: 20px auto;
  }

  @keyframes spin {
      0% { transform: rotate(0deg); }
      100% { transform: rotate(360deg); }
  }

  .user-image {
    margin: 20px auto;
  }
</style>
