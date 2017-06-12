
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
        <ul>
          <li v-for="ta in tab">
            <div class = "screen" v-for="t in ta" v-bind:style="{visibility:t.hide,backgroundColor:t.color}"></div>
          </li>
        </ul>
      </div>
    </div>
    <b-button @click="Start">Start</b-button>
  </div>
</template>

<script>
export default {
  name: 'hello',
  data () {
    return {
      list: [
        [{hide: '', color: 'white'}, {hide: '', color: 'red'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}],
        [{hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}],
        [{hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}],
        [{hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}, {hide: '', color: 'white'}]
      ],
      tabs: [
        [
          [{hide: 'hidden', color: '#FFFF00'}, {hide: '', color: '#FFFF00'}],
          [{hide: '', color: '#FFFF00'}, {hide: '', color: '#FFFF00'}]
        ],
        [
          [{hide: '', color: '#336633'}, {hide: 'hidden', color: '#336633'}],
          [{hide: '', color: '#336633'}, {hide: '', color: '#336633'}]
        ],
        [
          [{hide: '', color: '#CC6666'}, {hide: '', color: '#CC6666'}],
          [{hide: 'hidden', color: '#CC6666'}, {hide: '', color: '#CC6666'}]
        ],
        [
          [{hide: '', color: '#6633CC'}, {hide: '', color: '#6633CC'}],
          [{hide: '', color: '#6633CC'}, {hide: 'hidden', color: '#6633CC'}]
        ]
      ]
    }
  },
  methods: {
    Start () {
      var len = this.list.length / 2 - 1
      var list = this.list
      for (var i in list) {
        for (var j in list[i]) {
          if (list[i][j].color === 'red') {
            var num = i <= len && j <= len ? 0 : i > len && j <= len ? 1 : i <= len && j > len ? 2 : 3
            console.log(num)
          }
        }
      }
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
