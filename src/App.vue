<script>
import PlayersCard from './components/PlayersCard.vue';
import TeamCard from './components/TeamCard.vue';

export default {
  name: 'App',
  components: { PlayersCard, TeamCard },
  data: () => ({
    name: '',
    power: 0,
    players: [],
    team1: [],
    team2: [],
  }),
  methods: {
    addPlayer() {
      if (!this.name.length) return;

      this.players = [...this.players, { name: this.name, power: this.power }];
      this.resetInputs();
      this.focusToNameInput();
    },
    resetInputs() {
      this.name = '';
      this.power = 0;
    },
    resetFields() {
      this.players = [];
      this.team1 = [];
      this.team2 = [];
      this.resetInputs();
      this.focusToNameInput();
    },
    focusToNameInput() {
      this.$nextTick(() => {
        this.$refs.nameRef.focus();
      });
    },
    deletePlayer(player) {
      // Any suggestion for this method is welcome.
      if (this.players.some((item) => item === player)) {
        this.players = this.removePlayerFromList(this.players, player);
      } else if (this.team1.some((item) => item === player)) {
        this.team1 = this.removePlayerFromList(this.team1, player);
      } else if (this.team2.some((item) => item === player)) {
        this.team2 = this.removePlayerFromList(this.team2, player);
      }
    },
    removePlayerFromList(list, player) {
      list.splice(list.findIndex((item) => item === player), 1);

      return list;
    },
  },
};
</script>

<template>
<v-app>
  <v-container fill-height fluid class="main">
    <v-row>
      <v-col>
        <span> Create Team </span>

        <v-btn small dark @click="resetFields">
          RESET
        </v-btn>
      </v-col>
    </v-row>

    <v-row>
      <v-col cols="10">
        <v-text-field
          v-model="name"
          ref="nameRef"
          label="Player Name"
          dense
          hide-details
          @keyup.enter="addPlayer"
        />
      </v-col>

      <v-col cols="2">
        <v-text-field
          v-model="power"
          label="Power"
          dense
          hide-details
          @keyup.enter="addPlayer"
        />
      </v-col>
    </v-row>

    <v-row>
      <v-col>
        <players-card
          title="Players"
          :list="players"
          group="players"
          @deletePlayer="deletePlayer"
        />
      </v-col>
    </v-row>

    <v-row>
      <v-col style="text-align: center">
        <team-card
          title="Team 1"
          :list="team1"
          group="players"
          teamColor="blue"
          @deletePlayer="deletePlayer"
        />
      </v-col>

      <v-col>
        <team-card
          title="Team 2"
          :list="team2"
          group="players"
          teamColor="red"
          @deletePlayer="deletePlayer"
        />
      </v-col>
    </v-row>
  </v-container>
  </v-app>
</template>

<style lang="scss" scoped>
.main {
  max-width: 768px;
}
</style>
