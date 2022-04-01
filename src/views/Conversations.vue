<template>
<div>
  <Header />
  <section class="section">
    <template v-for="conversation in conversations">
      <Conversation :key="conversation.id" :conversation="conversation" />
    </template>
  </section>
  </div>
</template>

<script>
import Connexion from './Connexion.vue';
import Conversation from "../components/Conversation.vue";
import PosterMessage from '../components/PosterMessage.vue';
//import Header from "../components/Header.vue";

export default {
  components : {
    //Header,
    Conversation,
    PosterMessage,
    Connexion
  },
  data() {
    return {
      conversations : []
    };
  },
  mounted() {
    this.$api
    .get("channels")
    .then((response) => {
      this.conversations = response.data;
    });
  },
};
</script>;

<style>

</style>