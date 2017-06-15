
<template>
  <div class="hello">
    <p v-for="li in list">
      <ul>
        <li v-for="l in li">
          <div class = "screen" v-bind:class="l.color" v-bind:style="{backgroundColor:l.color}"></div>
        </li>
      </ul>
    </p>
    <div class="tabs">
      <div class="tab" v-for="tab in tabs">
        <ul  v-for="ta in tab">
          <li v-for="t in ta">
            <div class = "screen" v-bind:style="{visibility:t.hide,backgroundColor:t.color}"></div>
          </li>
        </ul>
      </div>
    </div>
    <b-button @click="Start(list)">Start</b-button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      list: [
        [{hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'red'}, {hide: '', color: 'white'}],
        [{hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}],
        [{hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}],
        [{hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}]
      ],
      tabs: [
        [
          [{hide: 'hidden', color: 'white'}, {hide: '', color: '#FFFF00'}],
          [{hide: '', color: '#FFFF00'}, {hide: '', color: '#FFFF00'}]
        ],
        [
          [{hide: '', color: '#336633'}, {hide: 'hidden', color: 'white'}],
          [{hide: '', color: '#336633'}, {hide: '', color: '#336633'}]
        ],
        [
          [{hide: '', color: '#CC6666'}, {hide: '', color: '#CC6666'}],
          [{hide: 'hidden', color: 'white'}, {hide: '', color: '#CC6666'}]
        ],
        [
          [{hide: '', color: '#6633CC'}, {hide: '', color: '#6633CC'}],
          [{hide: '', color: '#6633CC'}, {hide: 'hidden', color: 'white'}]
        ]
      ],
      nums: 0
    }
  },
  methods: {
    Start: function (list) {
      for (var i in list) {
        for (var j in list[i]) {
          if (list[i][j].color !== 'white') {
            var row = i
            var col = j
            console.log(i, j)
          }
        }
      }
      this.ChessBoard(0, 0, row, col, 4)
    },
    ChessBoard: function (tr, tc, dr, dc, size) {
      var s
      if (size === 1) {
        return
      }
      s = size / 2
      if (dr < tr + s && dc < tc + s) {
        this.fill(tr + s - 1, tc + s - 1, this.list, this.tabs[0])
        this.ChessBoard(tr, tc, dr, dc, s)
        this.ChessBoard(tr, tc + s, tr + s - 1, tc + s, s)
        this.ChessBoard(tr + s, tc + s, tr + s, tc + s, s)
        this.ChessBoard(tr + s, tc, tr + s, tc + s - 1, s)
      }
      if (dr < tr + s && dc >= tc + s) {
        this.fill(tr + s - 1, tc + s - 1, this.list, this.tabs[1])
        this.ChessBoard(tr, tc + s, dr, dc, s)
        this.ChessBoard(tr, tc, tr + s - 1, tc + s - 1, s)
        this.ChessBoard(tr + s, tc, tr + s, tc + s - 1, s)
        this.ChessBoard(tr + s, tc + s, tr + s, tc + s, s)
      }
      if (dr >= tr + s && dc < tc + s) {
        this.fill(tr + s - 1, tc + s - 1, this.list, this.tabs[2])
        this.ChessBoard(tr + 1, tc, dr, dc, s)
        this.ChessBoard(tr, tc, tr + s - 1, tc + s - 1, s)
        this.ChessBoard(tr, tc + s, tr + s - 1, tc + s, s)
        this.ChessBoard(tr + s, tc + s, tr + s, tc + s, s)
      }
      if (dr >= tr + s && dc >= tc + s) {
        this.fill(tr + s - 1, tc + s - 1, this.list, this.tabs[3])
        this.ChessBoard(tr + 1, tc + 1, dr, dc, s)
        this.ChessBoard(tr + s, tc, tr + s - 1, tc + s, s)
        this.ChessBoard(tr, tc, tr + s - 1, tc + s - 1, s)
        this.ChessBoard(tr, tc + s, tr + s - 1, tc + s, s)
      }
    },
    fill: (i, j, a1, a2) => {
      a1[i][j].color = a1[i][j].color === 'white' ? a2[0][0].color : a1[i][j].color
      a1[i][j + 1].color = a1[i][j + 1].color === 'white' ? a2[0][1].color : a1[i][j + 1].color
      a1[i + 1][j].color = a1[i + 1][j].color === 'white' ? a2[1][0].color : a1[i + 1][j].color
      a1[i + 1][j + 1].color = a1[i + 1][j + 1].color === 'white' ? a2[1][1].color : a1[i + 1][j + 1].color
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h1, h2 {
    font-weight: normal;
  }
  p{
    margin: 0;
    height: auto;
  }
  ul {
    list-style-type: none;
    padding: 0;
    margin: 0;
    line-height: 0;
  }

  li {
    display: inline-block;
    margin: 0 0px;
  }

  a {
    color: #42b983;
  }
  .screen{
    width: 50px;
    height: 50px;
    border:1px solid;
    border-color: #000;
    clear: both;
  }
  .tabs{
    display: flex;
    justify-content: center;
  }
  .tab{
    margin: 20px;
  }
</style>
