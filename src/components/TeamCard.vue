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
    totalPower: {
      type: Number,
      required: false,
      default: 0,
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
              draggable
              outlined
              label
              :style="{ borderColor: teamColor }"
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
