<script>
export default {
  created() {
    this.initField();
  },
  data () {
    return {
      flags: new Array(16).fill(0).map(() => new Array(16).fill(false)),
      choosen: new Array(16).fill(0).map(() => new Array(16).fill(true)),
      questions: new Array(16).fill(0).map(() => new Array(16).fill(true)),
      table: new Array(16).fill(0).map(() => new Array(16).fill(1)),
      mines: new Array(16).fill(0).map(() => new Array(16).fill(true)),
    }
  },
  methods: {
    getNeighboringMines(y, x) {
      const moves = [[1, 1], [1, 0], [0, 1], [-1, -1], [-1, 0], [0, -1]];
      return moves.filter(([x, y]) => this.mines[y][x]);
    },
    initField() {
      const bombs = 16;
      const cols = 16;
      const rows = 16;
      const size = rows * cols;
      const grid = [];
      /*for (let i = 0; i < size; i += 1) {
        grid.push({
          hasBomb: false,
          isOpen: false,
          hasFlag: false,
          bombCount: 0,
          neighborhood: null,
        });
      }*/
      while (bombs > 0) {
        const num = Math.floor(Math.random() * size);
        console.log(1, [Math.floor(num / 16)], [num % 16])
        if (this.mines[Math.floor(num / 16)][num % 16] == false) {
          bombs -= 1;
          this.mines[num / 16][num % 16] = true;
        }
      }
    }
  },
}
</script>

<template>
  <header>
    
  </header>

  <main>
    <div class="game">
      <div class="score"></div>
      <div class="field">
        <div class="row" v-for="row, y in table">
          <div class="ceil" v-for="ceil, x in row">
            <div class="sprite sprite-field-flag" v-if="flags[y][x]"></div>
            <div class="sprite sprite-field-mine" v-else-if="choosen[y][x] && mines[y][x]"></div>
            <div class="sprite sprite-field-question-choosen" v-else-if="choosen[y][x] && questions[y][x]"></div>
            <div class="sprite sprite-field-question" v-else-if="!choosen[y][x] && questions[y][x]"></div>
            <div class="sprite sprite-field-blank" v-else-if="!choosen[y][x]"></div>
            <div class="sprite" :class="'sprite-field-'+getNeighboringMines[y][x]" v-else></div>

          </div>
        </div>
      </div>
    </div>




    <!--div class="sprite sprite-table-1"></div>
    <div class="sprite sprite-table-2"></div>
    <div class="sprite sprite-table-3"></div>
    <div class="sprite sprite-table-4"></div>
    <div class="sprite sprite-table-5"></div>
    <div class="sprite sprite-table-6"></div>
    <div class="sprite sprite-table-7"></div>
    <div class="sprite sprite-table-8"></div>
    <div class="sprite sprite-table-9"></div>
    <div class="sprite sprite-table-0"></div>

    <div class="sprite sprite-field-1"></div>
    <div class="sprite sprite-field-2"></div>
    <div class="sprite sprite-field-3"></div>
    <div class="sprite sprite-field-4"></div>
    <div class="sprite sprite-field-5"></div>
    <div class="sprite sprite-field-6"></div>
    <div class="sprite sprite-field-7"></div>
    <div class="sprite sprite-field-8"></div>

    <div class="sprite sprite-field-blank"></div>
    <div class="sprite sprite-field-choosen"></div>
    <div class="sprite sprite-field-flag"></div>
    <div class="sprite sprite-field-question"></div>
    <div class="sprite sprite-field-question-choosen"></div>
    <div class="sprite sprite-field-mine"></div>
    <div class="sprite sprite-field-mine-choosen"></div> 
    <div class="sprite sprite-field-mine-cross"></div>
    
    <div class="sprite sprite-face-smile"></div>
    <div class="sprite sprite-face-smile-choosen"></div>
    <div class="sprite sprite-face-O"></div>
    <div class="sprite sprite-face-glasses"></div>
    <div class="sprite sprite-face-dead"></div-->


  </main>
</template>

<style scoped>
.game {
  border: 10px solid #a5a5a5;
  width: 256px;
  height: 256px;

}
.row {
  width: 256px;
}
</style>
