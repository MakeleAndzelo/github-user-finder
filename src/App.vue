<template>
  <div id="app">
    <div class="field has-addons">
      <div class="control">
        <input class="input" type="text" placeholder="Find a github user" v-model="nickname">
      </div>
      <div class="control">
        <a class="button is-info" @click="openModal">
          Search
        </a>
      </div>
    </div>
    <modal v-if="isActive" class="is-active" :nickname="nickname" @closeModal="closeModal"></modal>
  </div>
</template>

<script>
  import Modal from './components/Modal.vue';

  export default {
    name: 'app',
    data() {
      return {
        nickname: '',
        isActive: false
      }
    },
    components: {
      Modal
    },
    methods: {
      openModal() {
        this.isActive = true;
      },
      closeModal() {
        this.isActive = false;
      }
    }
  }
</script>

<style>
    html,
    body {
        width: 100%;
        height: 100%;
    }

    #app {
        width: 100%;
        height: 100%;
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>
