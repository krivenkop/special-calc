<template>
  <transition name="fade">
    <div v-show="show">
      <div class="row">
        <div class="col">
          <h3 class="calc__title">Перегородка</h3>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label for="part-block-type">Выберите блок</label>
          <select name="part-block-type"
                  id="part-block-type"
                  v-model="data.curBlock">
            <option value="-1"
                    disabled
                    selected>
              Виберите тип блока
            </option>
            <option v-for="block in blockList"
                    :key="block.id"
                    v-bind:value="block.id">
              {{block.title}}
            </option>
          </select>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label for="length-part">Длина, м</label>
          <input name="length-part"
                 id="length-part"
                 v-model="data.len"
                 type="number"
                 placeholder="Длина(м)">
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'PartsPanel',
  props: ['data', 'show', 'blockList'],
};
</script>

<style scoped>

</style>
