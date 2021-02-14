<template>
<select v-model="selectedArea">
  <option disabled value="">地域を選択</option>
  <option v-for="area in optionAreas" 
    v-bind:value="area.name" 
    v-bind:key="area.id"
    @click="setItems">
  {{ area.name }}
  </option>
</select>
<select v-model="selectedItem">
  <option disabled value="">名産品を選択</option>
  <option v-for="item in optionItems" 
    v-bind:value="item.name" 
    v-bind:key="item.id"
    @click="clickItem(item.name)"
  >
  {{ item.name }}
  </option>
</select>
<div id="map">
<span id="tokushima" @click="clickArea(1)"><a class="link_poi">徳島</a><br>{{selectedItemOnMap[0]}}</span>
<span id="ehime"     @click="clickArea(2)"><a class="link_poi">愛媛</a><br>{{selectedItemOnMap[1]}}</span>
<span id="kouchi"    @click="clickArea(3)"><a class="link_poi">高知</a><br>{{selectedItemOnMap[2]}}</span>
<span id="kagawa"    @click="clickArea(4)"><a class="link_poi">香川</a><br>{{selectedItemOnMap[3]}}</span>
<img id="shikoku" alt="shikoku" src="./assets/shikoku.png">
</div>
</template>

<script>

export default {
  data() {
    return {
      selectedItemOnMap: ['','','',''],
      selectedArea: '', 
      selectedItem: '',
      optionAreas: [ 
          { id: 1, name: '徳島' }, 
          { id: 2, name: '愛媛' }, 
          { id: 3, name: '高知' },
          { id: 4, name: '香川' }
      ],
      optionItems: [],
      itemsList: [
        [
          { id: 1, name: 'すだち' }, 
          { id: 2, name: '阿波おどり' }, 
          { id: 3, name: '渦潮' }
        ],
        [
          { id: 1, name: 'みかん' }, 
          { id: 2, name: '道後温泉' }, 
          { id: 3, name: '正岡子規' }         
        ],
        [
          { id: 1, name: 'ゆず' }, 
          { id: 2, name: '鰹のたたき' }, 
          { id: 3, name: '坂本龍馬' }
        ],
        [
          { id: 1, name: '讃岐うどん' }, 
          { id: 2, name: '金刀比羅宮' }, 
          { id: 3, name: 'オリーブ' }
        ]
      ]
    }
  },
  methods: {
    setItems:function(){
      const area_id = this.optionAreas.filter(e => e.name === this.selectedArea)[0].id
      this.optionItems = this.itemsList[area_id-1]
    },
    clickArea:function(area_id){
      this.optionItems = this.itemsList[area_id-1]
      this.selectedArea = this.optionAreas[area_id-1].name
    },
    clickItem:function(item_name){
      const area_id = this.optionAreas.filter(e => e.name === this.selectedArea)[0].id
      this.selectedItemOnMap[area_id-1] = item_name
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#map{
  margin: auto;
  width: 600px;
  height: 600px;
  position: relative;
}
#tokushima {
  position: absolute; top:200px; left:450px;
}
.link_poi{
  cursor: pointer;
  border: none;
  background: none;
  color: #0033cc;
}
.link_poi:hover{
  text-decoration: underline;
  color: #002080;
}
#ehime {
  position: absolute; top:230px; left:160px;
}
#kouchi {
  position: absolute; top:270px; left:270px;
}
#kagawa {
  position: absolute; top:150px; left:380px;
}
#shikoku{
  z-index: -1;
}
</style>
