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
  },
};
</script>

<template>
  <v-card elevation="2">
    <v-card-title> {{ title }}</v-card-title>

    <v-card-text>
      <draggable
        class="list-group"
        :list="list"
        :group="group"
        style="min-height: 128px;"
      >
        <template v-for="(player, index) in list">
          <v-chip
            id="chip"
            draggable
            outlined
            label
            :key="index"
          >
            {{ player.name }} - {{ player.power }}
          </v-chip>
        </template>
      </draggable>
    </v-card-text>
  </v-card>
</template>

<style scoped lang="scss">
  #chip {
    margin: 4px;
    border-color: black;
  }
</style>
