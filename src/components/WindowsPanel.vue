<template>
  <transition name="fade">
    <div v-show="show">
      <div class="row">
        <div class="col">
          <h3 class="calc__title">Окна</h3>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label for="height-w">Высота, м</label>
          <input name="height-w"
                 id="height-w"
                 v-model="windowsSize.height"
                 type="number"
                 placeholder="Высота окна(м)">
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label for="width-w">Ширина, м</label>
          <input name="width-w"
                 id="width-w"
                 v-model="windowsSize.width"
                 type="number"
                 placeholder="Ширина окна(м)">
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label for="count-w">Кол-во</label>
          <input name="count-w"
                 id="count-w"
                 v-model="windowsSize.count"
                 type="number"
                 placeholder="Кол-во">
        </div>
      </div>

      <div class="row">
        <div class="col">
          <h3 class="calc__title">Двери</h3>
        </div>
      </div>

      <div class="row">
        <div class="col">
          <label for="height-d">Высота, м</label>
          <input name="height-d"
                 id="height-d"
                 v-model="doorsSize.height"
                 type="number"
                 placeholder="Высота двери(м)">
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label for="width-d">Ширина, м</label>
          <input name="width-d"
                 id="width-d"
                 v-model="doorsSize.width"
                 type="number"
                 placeholder="Ширина двери(м)">
        </div>
      </div>
      <div class="row">
        <div class="col">
          <label for="count-d">Кол-во</label>
          <input name="count-d"
                 id="count-d"
                 v-model="doorsSize.count"
                 type="number"
                 placeholder="Кол-во">
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'WindowsPanel',
  props: ['doorsSize', 'windowsSize', 'show'],
};
</script>

<style scoped>

</style>
