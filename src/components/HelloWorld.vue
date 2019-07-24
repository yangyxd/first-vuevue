<template>
  <div class="hello">

      <div class="title">
        {{title}}<i class="iconfont icon-guanbi right"></i>
      </div>
      <ul class="list-group">
        <div style="margin-bottom: 20px; padding-bottom: 16px; border-bottom: solid #ccc 1px;">
          <span class="item-t">单位名称 : </span>
          <input type="text" v-model="unitName" class="name" style="width: 360px;" @keydown="addUnit" />
        </div>
        <div v-for="(item,i) in items" :key="i" class="item">
          <span class="item-t">{{item.title}} : </span>
          <input type="text" v-model="item.name" class="name" />
          <span> = </span>
          <input type="text" v-model="item.p1" class="p1" />
          <span> x </span>
          <select v-model="item.p2" @change="getUnitsSelected(item.p2)">
            <option :value="v" v-for="(v, i) in units" :key="i">{{v}}</option>
          </select>
        </div>
      </ul>

      <button btn-type="primary" class="btn btn-1" v-on:click="add">添加辅助单位 +</button>
      <button btn-type="primary" class="btn btn-primary" v-on:click="save" style="margin-bottom: 20px">alt + s / 保存</button>

  </div>
</template>

<script>
// import vueButton from "./button";
export default {
  name: 'HelloWorld',
  // components: {
  //       vueButton
  // },
  data: function () {
    return {
      title: '商品单位',
      items: [
        {title: '辅助单位1', name: '101 新增单位', p1: 1, p2: '新增单位'},
        {title: '辅助单位2', name: '102 新增单位', p1: 2, p2: '新增单位'}
      ],
      units: [
        '新增单位',
        '其它单位'
      ],
      unitName: '101 新增单位'
    }
  },
  methods: {
    add: function () {
      var i = this.items.length
      i++
      this.items.push(
        {
          title: '辅助单位' + i,
          name: (i + 100) + ' 新增单位',
          p1: i,
          p2: '新增单位'
        }
      )
    },
    save: function () {
      alert('保存成功')
    },
    keypressEvent (e) {
      if (e.altKey === true && e.keyCode === 83) {
        this.save()
      }
    },
    getUnitsSelected (v) {
      this.unitName = v
    },
    addUnit: function (ev) {
      if (ev.keyCode === 13) {
        if (this.units.indexOf(this.unitName) < 0) {
          this.units.push(this.unitName)
        }
      }
    }
  },
  created: function () {
    document.addEventListener('keydown', this.keypressEvent)
  },
  destroyed: function () {
    document.removeEventListener('keydown', this.keypressEvent)
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.hello {
  width: 512px;
  height: auto;
  padding: 0px 12px;
  border: solid #ccc 1px;
  align-content: center;
  margin: auto;
}
.title {
  color: #1b4b74;
  font-weight: 600;
  height: 50px;
  border-bottom: solid #ccc 1px;
  text-align: start;
  vertical-align: center;
  line-height: 50px;
}
.right {
  float: right;
  position:inherit;
}
.item {
  font-size: 14px;
  padding: 4px 8px;
  text-align: left;
  overflow: hidden;
  display: inline-block;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.list-group {
  margin-top: 20px;
  padding: 0px;
  width: 100%;
  float: left;
}
.list-group input, select {
  color: #0099cc;
  padding: 4px;
  line-height: 22px;
  font-size: 14px;
}
select {
  height: 35px;
  margin-left: 4px;
  margin-right: 4px;
  width: 120px;
}
.item span {
  margin-left: 4px;
  margin-right: 4px;
}
.item-t {
  margin-right: 4px;
}
.item .name{
  position: inherit;
  width: 120px;
  padding-left: 8px;
}
.item .p1 {
  width: 70px;
  text-align: center;
}
.item .p2 {
  width: 155px;
  padding-left: 8px;
}
.btn-1 {
  width: 95%;
  background-color: #e8f6ff;
  border: solid #666 1px;
  border-radius: 5px;
  min-height: 30px;
  color: #333;
  margin-bottom: 20px;
}
a {
  color: #42b983;
}
</style>
