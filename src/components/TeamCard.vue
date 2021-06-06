<script>
import draggable from 'vuedraggable';

export default {
  name: 'TeamCard',
  components: { draggable },
  props: {
    title: {
      type: String,
      required: true,
    },
    list: {
      type: Array,
      required: true,
    },
    group: {
      type: String,
      required: true,
    },
    teamColor: {
      type: String,
      require: true,
    },
  },
  computed: {
    totalPower() {
      return this.list
        .map((item) => Number(item.power))
        .reduce((a, b) => a + b, 0);
    },
  },
};
</script>

<template>
  <v-card elevation="2">
    <v-card-title> {{ title }} - {{ totalPower }} </v-card-title>

    <v-card-text>
      <draggable
        class="list-group"
        :list="list"
        :group="group"
        style="min-height: 128px;"
      >
        <template v-for="(player, index) in list">
          <v-row :key="index">
            <v-chip
              id="chip"
              :style="{ borderColor: teamColor }"
              draggable outlined label
              close
              close-icon="mdi-close-outline"
              @click:close="$emit('deletePlayer', player)"
            >
              {{ player.name }} - {{ player.power }}
            </v-chip>
          </v-row>
        </template>
      </draggable>
    </v-card-text>
  </v-card>
</template>

<style scoped lang="scss">
  #chip {
    margin: auto;
    margin-top: 4px;
    margin-bottom: 4px;
  }
</style>
