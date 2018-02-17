<template>
  <transition name="fade">
    <div v-show="show">
      <div class="row">
        <div class="col">
          <div class="result">
            <h3 class="calc__title">Результат</h3>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <p>Обьем кладки: {{ wallVolume.toFixed(2) }}м.куб.</p>
          <p>Без окон: {{ (wallVolume - windowsVolume).toFixed(2) }}</p>
          <p>Кол-во блоков для перегородки: {{ countPartBlocks }}</p>
          <p>Кол-во блоков для кладки: {{ countBlocks }}</p>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: 'Result',
  props: [
    'show',
    'wallVolume',
    'windowsVolume',
    'countPartBlocks',
    'countBlocks',
  ],
};
</script>

<style scoped >
</style>
