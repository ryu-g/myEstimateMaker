<template lang="pug">
#app
  .metaInfo
    .meta
      .number
        p 御見積番号 : 
        p.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") 000000
      .date
        p 発行日 : 
        p.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") 0000

  h1 {{ datalist.msg }}
  .information
    ul.direction
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{ datalist.direction.company }}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") 〒 {{ datalist.direction.postalCode }}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{ datalist.direction.address1 }}
      //- li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{ direction.address2 }}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{ datalist.direction.person }}
    ul.from
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{datalist.from.company}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") 〒 {{datalist.from.postalCode}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{ datalist.from.address1}}
      //- li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{from.address2}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") TEL : {{ datalist.from.phone}}
      //- li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{from.fax}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") MAIL : {{ datalist.from.Email}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") 担当 : {{ datalist.from.person}}

  .estimatePrice
    ul.table
      li.payHeading 御見積り金額
      li.payItem {{ datalist.total }} 円
    ul.table
      li.heading.number Main Tag.
      li.heading.number sub tag.
      //- li.heading.date 年 / 月 / 日
      li.heading.name 品目名
      li.heading 単価
      li.heading 数量
      li.heading 金額

    div#sortable
      ul.table(v-for = "(value, key) in datalist.object")
        li.item.number.editable.editableitem(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'mainNo')") {{ value.mainNo }}
        li.item.number.editable.editableitem(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'subNo')") {{ value.subNo }}
        //- li.item.date.editable.editableitem(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'date')") {{ value.date }}
        li.item.name.editable.editableitem(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'name')") {{ value.name }}
        li.item.price.editable.editableitem(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'price')") {{ value.price }}
        li.item.amount.editable.editableitem(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'num')") {{ value.num }}
        li.item.subtotal(contenteditable='false' @blur="onBlur($event, key, 'sum')") {{ value.sum }}

    ul.table
      li.addItem ADD
      li.deleteItem DELETE
      li.result.subAmount 小計
      li.item.subAmount {{ datalist.subtotal }}

      li.result.tax 消費税(8%)
      li.item.tax {{ datalist.tax }}

      li.result.total 合計
      li.item.total {{ datalist.total }}

  .other
    .option
      h4 支払条件
      p.editable(contenteditable = "true" onclick="document.execCommand('selectAll',false,null)" ) あいうえお
    .option
      h4 振込手数料負担
      p.editable(contenteditable = "true" onclick="document.execCommand('selectAll',false,null)") 御社にてご負担願います
    .option
      h4 有効期限
      p.editable(contenteditable = "true" onclick="document.execCommand('selectAll',false,null)") 発行日から2019/2/1まで
    .option
      h4 備考
      p.editable(contenteditable = "true" onclick="document.execCommand('selectAll',false,null)") ほげほげ
</template>

<script>
 import 'normalize.css'
import Sortable from 'sortablejs'
import itemdata from './assets/aqreate-web.json'

let vm

export default {
  name: 'app',
  data () {
    return {
      datalist : itemdata 
    }
  },

  mounted () {
    vm = this
    vm.getDatas()
    let editable = document.getElementsByClassName('editableitem')
    // document.getElementsByClassName('total')[0].addEventListener(('click'), () => {console.log(vm)})

    document.getElementsByClassName('addItem')[0].addEventListener(('click'), vm.addItem)
    document.getElementsByClassName('deleteItem')[0].addEventListener(('click'), vm.deleteItem)

    const el = document.getElementById('sortable')  
    const sortable = Sortable.create(el,{
      animation: 150,
      onEnd: ()=> {
        console.log("end dragging")
        editable = document.getElementsByClassName('editableitem')
        for(let i=0 ; i < editable.length ; i++){
          // editable[i].removeEventListener(('click'), vm.editableMakeTrue)
          // editable[i].removeEventListener(('mouseleave'), vm.editableMakeFalse )
          editable[i].addEventListener(('click'), function(){vm.editableMakeTrue(i)})
          editable[i].addEventListener(('mouseleave'),function(){vm.editableMakeFalse(i)})
        }
      }
    })
    // for(let i=0 ; i < editable.length ; i++){
    //   editable[i].addEventListener(('click'), function(){vm.editableMakeTrue(i)})
    //   editable[i].addEventListener(('mouseleave'),function(){vm.editableMakeFalse(i)})
    // }
    for(let i=0 ; i < editable.length ; i++){
      editable[i].addEventListener(('click'), function(){vm.editableMakeTrue(i)})
      editable[i].addEventListener(('mouseleave'),function(){vm.editableMakeFalse(i)})
    }
  },

  methods: {
    getDatas: ()=>{
      console.log("オブジェクト内のデータを計算して各数値を更新します")
      let sum = 0

      let price
      let num
      for(const i in vm.datalist.object){
        vm.datalist.object[i].sum = vm.removeLetter(vm.datalist.object[i].price) * vm.removeLetter(vm.datalist.object[i].num)
        sum += vm.removeLetter(vm.datalist.object[i].sum)
        vm.datalist.object[i].sum = vm.datalist.object[i].sum.toLocaleString()
      }
      vm.datalist.subtotal = sum.toLocaleString()          // add camma to subtotal
      const subs = vm.removeLetter(vm.datalist.subtotal)      // shrink subtotal
      vm.datalist.tax = Math.floor(subs * vm.datalist.taxRatio - subs) // calc tax
      vm.datalist.tax = vm.datalist.tax.toLocaleString()                // add camma to tax
      vm.datalist.total = (vm.removeLetter(subs) + vm.removeLetter(vm.datalist.tax)).toLocaleString() //calc total
    },
    addItem(){
      let editable = document.getElementsByClassName('editableitem')
      console.log("clicked ADD")
      const newData =
        {
          mainNo: "999",
          subNo: 999,
          date: "2018/12/31",
          name: 'sample',
          price: 10000,
          num: 1,
          sum: 0
        }
      console.table(newData)
      const index = this.datalist.object.length
      console.log("object length is " + this.datalist.object.length)
      vm.$set(this.datalist.object, index, newData)
      for(let i = editable.length-5; i < editable.length ; i++){
        editable[i].addEventListener(('click'), function(){vm.editableMakeTrue(i)})
        editable[i].addEventListener(('mouseleave'),function(){vm.editableMakeFalse(i)})
        //console.log(editable[i+5]);
      }
      vm.getDatas()
    },
    deleteItem(){
      console.log("clicked Delete")
      const index = this.datalist.object.length
      // vm.$delete(this.datalist.object, index)
      vm.datalist.object.splice(index-1, 1)
      console.log("delete target object length is " + this.datalist.object.length)
      vm.getDatas()
    },

    a(){ editableMakeTrue:(i)=>{
      let editable = document.getElementsByClassName('editableitem')
      editable[i].contentEditable = 'true'
    } },
    b(){ editableMakeFalse:(i)=>{
      let editable = document.getElementsByClassName('editableitem')
      editable[i].contentEditable = 'false'
    } },
    editableMakeTrue(i){
      let editable = document.getElementsByClassName('editableitem')
      editable[i].contentEditable = 'true'
      // console.log(i+ " : " + editable[i].contentEditable)
      // console.log("hello morning");
    },
    editableMakeFalse(i){
      let editable = document.getElementsByClassName('editableitem')
      editable[i].contentEditable = 'false'
      console.log(i+ " : " + editable[i].contentEditable)
    },

    removeLetter: (txt) => {
      if(isNaN(txt)){
        let replaced = txt.replace(/[^0-9]/g, '')
        return Number(replaced)
      }
      return Number(txt)
    },

    //数字入力欄のフォーカス解除時発火
    onBlur: (e, i, param) => {
      vm.datalist.object[i][param] = e.target.innerText
      if (param === 'num' || param === 'price') {
        let sum = 0

        vm.datalist.object[i][param] = vm.removeLetter(vm.datalist.object[i][param]).toLocaleString()//異物を撮ってからComma追加
        e.target.innerText = vm.datalist.object[i][param]
        vm.datalist.object[i]['sum'] = vm.removeLetter(vm.datalist.object[i]['num']) * vm.removeLetter(vm.datalist.object[i]['price'])
        vm.datalist.object[i]['sum'] = Number(vm.datalist.object[i]['sum'])
        // calcurate datalist.subtotal with price by num
        for (const i in vm.datalist.object) {
          //console.log("[285]sum is : " + (vm.datalist.object[i].sum))
          sum += vm.removeLetter(vm.datalist.object[i].sum)
          vm.datalist.object[i].sum = vm.datalist.object[i].sum.toLocaleString()
          console.log("[287]added sum is  " + vm.removeLetter(sum))
        }
        console.log("-------")
        vm.datalist.subtotal = sum.toLocaleString()
        const subs = vm.removeLetter(vm.datalist.subtotal)
        console.log("subs: "+subs)
        vm.datalist.tax = Math.floor(subs * vm.datalist.taxRatio - subs)
        vm.datalist.tax = vm.datalist.tax.toLocaleString()
        vm.datalist.total = (vm.removeLetter(subs) + vm.removeLetter(vm.datalist.tax)).toLocaleString()
      }
    }
  }
}

</script>

<style lang ="stylus" scoped>

h1 h2 h3 h4 div p ul li
  margin 0
  padding 0

#app
  font-family  Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  display block
  width 100vw
  height 141.4vw
  border 1px solid #999
  margin 0 auto

  h1
    font-size 3vw
    font-weight normal
    padding 2vw 0 4vw 0
    margin 0
  h4
    font-size 1.4vw
    font-weight bold
    text-align left

ul
  list-style-type none
  padding 0
  margin 0

@media print
  #app
    width 100%
    height 141vw
    margin 0
    padding 0
  .addItem
  .deleteItem
    display none

.metaInfo
  display flex
  flex-direction row-reverse
  width 80%
  margin 40px auto 0 auto
  text-align left
  color #777
  p
    font-size 1.2vw
    margin .5vw .25vw 
  .meta
    display flex
    flex-direction column
    .number
    .date
      display flex
      flex-direction default
    
.information
  width 80%
  margin 20px auto
  display flex
  text-align left

  .direction
    width 50%
    li
      font-size 1.2vw
      line-height: 2.5vw
  .from
    width 50%
    margin-left 20px
    li
      font-size 1.1vw
      line-height: 2.0vw

.estimatePrice
  width 90%
  margin 3vw auto
  .table
    display grid
    // Main No., sub no. 年月日,品目名,単価,数量,金額
    grid-template-columns 1fr .8fr 4.6fr 1fr .8fr 1fr
    grid-gap .3vw .2vw
    margin .2vw 0
    li
      margin 0
      color #333
      padding .6vw .5vw
      font-size 1.4vw
      overflow hidden

    .addItem
      background-color #7CBF7F
      color white
      font-weight bold
      font-size 1.4vw
      align-items center
    .deleteItem
      background-color #B04F4F
      color white
      font-weight bold
      font-size 1.4vw
      align-items center

    .payHeading
      grid-column 1 / 3
      background-color #333
      color #fff
      font-weight bold
    .payItem
      grid-column 3 / 5
      background-color #eee
      font-weight bold

    .heading
      background-color #333
      color #eee
      font-weight bold
      font-size 1vw
      line-height 1vw
      display flex
      align-items center
      justify-content center

    .item
      display flex
      align-items center
      justify-content center
      background-color #eee
      font-size 1.3vw
      line-height 1.8vw
    .price
    .amount
    .subtotal
    .subAmount
    .tax
    .total
      justify-content flex-end

    .item.total
    .item.subAmount
    .item.tax
    .item.subtotal
      background-color: #ddd

    .result
      grid-column 4 / 6
      background-color #333
      color #eee
      font-weight bold
      font-size 1.4vw
      line-height 1.4vw
      display flex
      align-items center
      justify-content center

    .option
      grid-column 1 / 3
      font-size: 1.2vw
      line-height: 1.5vw

.other
  width 80%
  margin 0 auto
  //border solid 1px #aaa

  .option
    display flex
    align-items flex-start
    margin 2vw 0
    h4
      display block
      width 14vw
      margin 0
    p
      width 65vw
      font-size 1.4vw
      line-height 2vw
      text-align left
      margin 0

li.editable
p.editable
  cursor text
  transition .12s
  &:hover
    color #40A900
.sortable-chosen 
  color: #fff;
  background-color #40A900
  .item
    background-color #40A900

</style>
