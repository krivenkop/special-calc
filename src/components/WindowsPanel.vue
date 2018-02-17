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
          <input name="height"
                 v-model="windowsSize.height"
                 type="number"
                 placeholder="Высота окна(м)">
        </div>
      </div>
      <div class="row">
        <div class="col">
          <input name="width"
                 v-model="windowsSize.width"
                 type="number"
                 placeholder="Ширина окна(м)">
        </div>
      </div>
      <div class="row">
        <div class="col">
          <input name="length"
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
          <input name="height"
                 v-model="doorsSize.height"
                 type="number"
                 placeholder="Высота двери(м)">
        </div>
      </div>
      <div class="row">
        <div class="col">
          <input name="width"
                 v-model="doorsSize.width"
                 type="number"
                 placeholder="Ширина двери(м)">
        </div>
      </div>
      <div class="row">
        <div class="col">
          <input name="length"
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
