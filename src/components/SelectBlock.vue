<template>
  <select name="block-type"
          v-model="currentBlockId"
          @change="onSelectOption()">
    <!--<option value="-1"-->
            <!--disabled-->
            <!--selected>-->
      <!--Виберите тип блока-->
    <!--</option>-->
    <option v-for="block in blockList"
            :key="block.id"
            v-bind:value="block.id">
      {{block.title}}
    </option>
  </select>
</template>

<script>
/* eslint-disable no-console */

export default {
  name: 'SelectBlock',
  props: ['blockList'],
  data() {
    return {
      currentBlockId: 1,
    };
  },
  methods: {
    onSelectOption() {
      this.$emit('block-selected', this.currentBlockId);
    },
  },
};
</script>

<style scoped lang="sass">

</style>
