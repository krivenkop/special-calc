<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col-lg-6">

          <form action="#" class="calc__form">

            <div class="row">
              <h2>Калькулятор</h2>
            </div>
            <div class="row">
              <div class="col">
                <input name="height"
                       v-model="boxSize.height"
                       type="number"
                       placeholder="Высота(кирпичи)">
                <p class="height-metres">{{ boxParams.height }}м</p>

              </div>
            </div>
            <div class="row">
              <div class="col">
                <input name="width"
                       v-model="boxSize.width"
                       type="number"
                       placeholder="Ширина(м)">
              </div>
            </div>
            <div class="row">
              <div class="col">
                <input name="length"
                       v-model="boxSize.length"
                       type="number"
                       placeholder="Длина(м)">
              </div>
            </div>

            <div class="row">
              <div class="col">
                <SelectBLock :block-list="mainBlocks"
                              v-on:block-selected="onSelectMainBlock"/>
              </div>
            </div>

            <div class="row">
              <div class="col">
                <select name="block-half"
                        v-model="wallWidth">
                  <option selected="selected"
                          value="0.4">
                    Целый
                  </option>
                  <option value="0.2">Полблока</option>
                </select>
              </div>
            </div>

            <div class="row">
              <div class="col d-flex justify-content-center flex-row">
                <p class="show-windows"
                   v-on:click="showWindowsPanel = !showWindowsPanel">
                  Окна и двери
                </p>
                <p class="show-parts"
                   v-on:click="showPartsPanel = !showPartsPanel">
                  Посчитать перегородки
                </p>
              </div>
            </div>

            <WindowsPanel :show="showWindowsPanel"
                          :windows-size.sync="windowsSize"
                          :doors-size.sync="doorsSize"/>

            <PartsPanel :show="showPartsPanel"
                        :data.sync="partsSize"
                        :block-list="partBlocks"/>
          </form>

        </div>
        <div class="col-lg-6">
          <Result :show="showResult"
                  :wall-volume="TotalWallVolume"
                  :windows-volume="getWindowsVolume"
                  :count-part-blocks="countPartBlocks"
                  :count-blocks="countBlocks"/>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable no-console,prefer-const */

import SelectBLock from './components/SelectBlock';
import WindowsPanel from './components/WindowsPanel';
import PartsPanel from './components/PartsPanel';
import Result from './components/Result';

export default {
  name: 'App',
  components: {
    SelectBLock,
    WindowsPanel,
    PartsPanel,
    Result,
  },
  data() {
    return {
      showWindowsPanel: false,
      showPartsPanel: false,
      currentBlock: 1,
      boxSize: {
        height: '',
        width: '',
        length: '',
      },
      windowsSize: {
        width: '',
        height: '',
        count: '',
      },
      doorsSize: {
        width: '',
        height: '',
        count: '',
      },
      partsSize: {
        curBlock: 1,
        len: '',
      },
      wallWidth: 0.4,
      mainBlocks: [
        {
          id: 1,
          title: 'КСЛ 35 (termolock)',
          length: 1200,
          width: 400,
          height: 400,
          weight: 170,
          size: '1200,400,400',
          amount: 0.192,
        },
        {
          id: 2,
          title: 'КСР 75 (восьмищелевой)',
          length: 400,
          width: 200,
          height: 200,
          weight: 14,
          size: '400,200,200',
          amount: 0.016,
        }],
      partBlocks: [
        {
          id: 1,
          title: 'КПР 50 (перегородочный)',
          length: 400,
          width: 90,
          height: 200,
          weight: 7,
          size: '400,90,200',
          amount: 0.0072,
        },
      ],
    };
  },
  methods: {
    onSelectMainBlock(id) {
      this.currentBlock = id;
    },
  },
  computed: {
    boxParams() {
      return {
        height: this.boxSize.height === '' ? 0 : (+this.boxSize.height *
          (this.getCurBlock.height / 1000)).toFixed(2),
        width: this.boxSize.width === '' ? 0 : +this.boxSize.width,
        len: this.boxSize.length === '' ? 0 : +this.boxSize.length,
      };
    },
    windowsParams() {
      return {
        height: this.windowsSize.height === '' ? 0 : +this.windowsSize.height,
        width: this.windowsSize.width === '' ? 0 : +this.windowsSize.width,
        count: this.windowsSize.count === '' ? 0 : +this.windowsSize.count,
      };
    },
    doorsParams() {
      return {
        height: this.doorsSize.height === '' ? 0 : +this.doorsSize.height,
        width: this.doorsSize.width === '' ? 0 : +this.doorsSize.width,
        count: this.doorsSize.count === '' ? 0 : +this.doorsSize.count,
      };
    },
    partsParams() {
      return {
        len: this.partsSize.len === '' ? 0 : +this.partsSize.len,
      };
    },
    getCurBlock() {
      const curBlock = this.currentBlock;
      return curBlock === -1 ? null : this.mainBlocks[+curBlock - 1];
    },
    getCurPartBlock() {
      const curBlock = this.partsSize.curBlock;
      return curBlock === -1 ? null : +curBlock;
    },
    showResult() {
      return Boolean(this.boxSize.height &&
              this.boxSize.width &&
              this.boxSize.length);
    },
    calcPartWallVolume() {
      return this.calcPartArea * this.wallWidth;
    },
    calcWallVolume() {
      return (2 * (this.boxParams.height *
        this.boxParams.len *
        this.wallWidth)) +
        (2 * ((this.boxParams.height *
          this.boxParams.width *
          this.wallWidth)));
    },
    TotalWallVolume() {
      return this.calcPartWallVolume + this.calcWallVolume;
    },
    getWindowsVolume() {
      return this.windowsParams.width *
        this.windowsParams.height *
        this.windowsParams.count *
        this.wallWidth;
    },
    calcPartArea() {
      return this.partsParams.len * this.boxParams.height;
    },
    calcPartBlockArea() {
      let partBlockId = this.getCurPartBlock;
      if (partBlockId === null) {
        return 0;
      }
      let curPartBlock = this.partBlocks[partBlockId - 1];
      return (curPartBlock.length * curPartBlock.height) / 100000;
    },
    countPartBlocks() {
      let clearPartArea = this.calcPartArea -
        (this.doorsParams.width *
          this.doorsParams.height *
          this.doorsParams.count);
      return Math.ceil(clearPartArea / this.calcPartBlockArea);
    },
    countBlocks() {
      return (this.TotalWallVolume / this.getCurBlock.amount).toFixed(2);
    },
  },
};
</script>

<style lang="sass">
  @import url('https://fonts.googleapis.com/css?family=Roboto')
  @import url('./assets/bootstrap-grid/grid.min.css')

  *
    -webkit-box-sizing: border-box
    -moz-box-sizing: border-box
    box-sizing: border-box
    &:before, &:after
      -webkit-box-sizing: border-box
      -moz-box-sizing: border-box
      box-sizing: border-box

  *::-webkit-input-placeholder
    color: #666
    opacity: 1

  *:-moz-placeholder
    color: #666
    opacity: 1

  *::-moz-placeholder
    color: #666
    opacity: 1

  *:-ms-input-placeholder
    color: #666
    opacity: 1

  body input:focus:required:invalid,
  body textarea:focus:required:invalid
    color: #666
  body input:required:valid,
  body textarea:required:valid
    color: #666

  html, body
    height: 100%

  body
    font-size: 16px
    min-width: 320px
    position: relative
    line-height: 1.65
    font-family: 'Roboto', sans-serif
    overflow-x: hidden

  .text-center
    text-align: center

  .result-container
    margin-top: 80px
    padding: 0 20px 30px 20px
    box-shadow: 3px 2px 10px 0 #666
    .calc__title
      display: block
      width: 100%
      text-align: center
      color: #444444
      margin-top: 0
      margin-bottom: 10px
      margin-top: 20px

  .calc__form
    display: block
    box-shadow: 3px 2px 10px 0 #666
    padding: 0 20px 30px 20px
    margin-top: 80px
    margin-bottom: 80px
    h2
      color: #333333
      text-align: center
      width: 100%
    input
      border: none
      background-color: transparent
      border-bottom: 2px solid #333
      width: 100%
      height: 26px
      font-size: 20px
      color: #333333
      outline-color: #666666
    input[type=number]::-webkit-inner-spin-button,
    input[type=number]::-webkit-outer-spin-button
      appearance: none
    select
      background-color: transparent
      border: 2px solid #333333
      height: 26px
      font-size: 20px
      color: #333333
    .row:not(:first-child)
      margin-top: 20px
    .show-windows
      cursor: pointer
      display: block
      padding: 5px 20px
      margin-right: 10px
      background-color: transparent
      border: 2px solid #222
      margin-bottom: 0
    .show-parts
      cursor: pointer
      display: block
      padding: 5px 20px
      margin-left: 10px
      background-color: transparent
      border: 2px solid #222
      margin-bottom: 0
    .calc__title
      display: block
      width: 100%
      text-align: center
      color: #444444
      margin-top: 0
      margin-bottom: 10px
    h3.calc__title
      margin-top: 20px
      margin-bottom: 0

</style>
