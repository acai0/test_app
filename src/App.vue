 <template>
  <div>
    <router-view v-if="$store.state.ready" />
    <template v-else>
      <div class="chargement has-text-align">
        <p>chargement, veuillez patienter</p>
        <button class="button is-loading is-dark"></button>
      </div>
    </template>
  </div>
</template>
<script>
export default {
  name: "App",
  mounted() {
     this.$store.commit("setReady", false);

    if(!this.$store.state.token) {
      this.seConnecter();
    }
    else{
      this.$api.get(`users/${this.$store.state.member.id}/signin`)
      .then(this.demarrer)
      .catch(this.seConnecter);
    }
  },

  methods: {
    ready(){
      this.$store.commit("setReady", true);
    },
    demarrer(){
        this.$api.get("members").then((response) => {
        this.$store.commit("setMembers", response.data);
        this.ready();
      });
    },
    seConnecter() {
        this.$store.commit("setToken", false);
        this.$router.push("/connexion");
        this.ready();
    }
  }
}
</script>
<style>
</style>