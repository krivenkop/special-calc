<template>
  <transition name="fade">
    <div class="result-container" v-show="show">
      <div class="row">
        <div class="col">
          <div class="result">
            <h2 class="calc__title">Результат</h2>
          </div>
        </div>
      </div>
      <div class="row">
        <div class="col">
          <p>Выбранный блок: {{ curBlock.title }}. Размеры {{ curBlock.size }}</p>
          <p>Площадь стен: {{ wallArea }}</p>
          <p>Кол-во блоков для кладки: {{ countBlocks }}</p>
          <p>Обьем кладки: {{ wallVolume.toFixed(2) }}м.куб.</p>
          <p>Цена за все блоки: {{ countBlocks * curBlock.total_price }}</p>
          <p>****************************************</p>
          <p>Без окон: {{ (wallVolume - windowsVolume).toFixed(2) }}</p>
          <p>Кол-во блоков для перегородки: {{ countPartBlocks }}</p>
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
    'wallArea',
    'windowsVolume',
    'countPartBlocks',
    'countBlocks',
    'curBlock',
  ],
};
</script>

<style scoped >
</style>
