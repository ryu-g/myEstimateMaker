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

  h1 {{ msg }}
  .information
    ul.direction
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{ direction.company }}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") 〒 {{ direction.postalCode }}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{ direction.address1 }}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{ direction.address2 }}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{ direction.person }}
    ul.from
      //- li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{from.company}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") 〒 {{from.postalCode}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{from.address1}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{from.address2}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") TEL : {{from.phone}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") {{from.fax}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") MAIL : {{from.Email}}
      li.editable(contenteditable = 'true' onclick="document.execCommand('selectAll',false,null)") 担当 : {{from.person}}

  .estimatePrice
    ul.table
      li.payHeading 御見積り金額
      li.payItem {{ total }} 円
    ul.table
      li.heading.number Main Tag.
      li.heading.number sub tag.
      li.heading.date 年 / 月 / 日
      li.heading.name 品目名
      li.heading 単価
      li.heading 数量
      li.heading 金額

    div#sortable
      ul.table(v-for = "(value, key) in object")
        li.item.number.editable(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'mainNo')") {{ value.mainNo }}
        li.item.number.editable(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'subNo')") {{ value.subNo }}
        li.item.date.editable(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'date')") {{ value.date }}
        li.item.name.editable(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'name')") {{ value.name }}
        li.item.price.editable(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'price')") {{ value.price }}
        li.item.amount.editable(contenteditable='false' ondblclick="document.execCommand('selectAll',false,null)" @blur="onBlur($event, key, 'num')") {{ value.num }}
        li.item.subtotal(contenteditable='false' @blur="onBlur($event, key, 'sum')") {{ value.sum }}

    ul.table
      li.addItem ADD
      li.deleteItem DELETE
      li.result.subAmount 小計
      li.item.subAmount {{ subtotal }}

      li.result.tax 消費税(8%)
      li.item.tax {{ tax }}

      li.result.total 合計
      li.item.total {{ total }}

  .other
    .option
      h4 支払条件
      p.editable(contenteditable = "true") あいうえお
    .option
      h4 振込手数料負担
      p.editable(contenteditable = "true") 御社にてご負担願います
    .option
      h4 有効期限
      p.editable(contenteditable = "true") 発行日から2019/2/1まで
    .option
      h4 備考
      p.editable(contenteditable = "true") ほげほげ
</template>

<script>
import 'normalize.css'
import Sortable from 'sortablejs'

let vm
export default {
  name: 'app',
  data () {
    return {
      msg: '御見積書',
      direction: {
        company: "beidp 御中",
        postalCode: "000-0000",
        address1: "東京都千代田区100-100-100",
        address2: "hogehogeの建物",
        person: "ご担当: hoge 様"
      },
      // from: {
      //   company: "",
      //   postalCode: "000-0000",
      //   address1: "函館市昭和1丁目3-40",
      //   address2: "サンビレッジ昭和ウェスト館108号",
      //   phone: "090-6870-8093",
      //   fax: "",
      //   Email: "em.ryu.g@gmail.com",
      //   person: "me"
      // },
      from: {
              company: "",
              postalCode: "000-0000",
              address1: "東京都千代田区1-1-1",
              address2: "hhhhhhhhhhhhhhhhhhhhhhhhhhhhhhhh",
              phone: "090-0909-09-09",
              fax: "9090990",
              Email: "gmail.com@gmail.com",
              person: "me"
            },
      object: [
        {
          mainNo: 1,
          subNo: 1,
          date: "2018/12/31",
          name: 'CMS導入',
          price: 0,
          num: 1,
          sum: 0
        },
        {
          mainNo: 2,
          subNo: 1,
          date: "2018/12/31",
          name: 'トップページデザイン',
          price: '50,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: "",
          subNo: 2,
          date: "2018/12/31",
          name: '会社紹介ページデザイン',
          price: '20,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: "",
          subNo: 3,
          date: "2018/12/31",
          name: 'お知らせページデザイン',
          price: '20,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: "",
          subNo: 4,
          date: "2018/12/31",
          name: '実績一覧ページデザイン',
          price: '20,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: "",
          subNo: 5,
          date: "2018/12/31",
          name: '実績個別ページデザイン',
          price: '20,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: "",
          subNo: 6,
          date: "2018/12/31",
          name: 'お問い合わせページデザイン',
          price: '20,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: 3,
          subNo: 1,
          date: "2018/12/31",
          name: 'トップページ開発',
          price: '30,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: "",
          subNo: 2,
          date: "2018/12/31",
          name: '会社紹介ページ開発',
          price: '20,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: "",
          subNo: 3,
          date: "2018/12/31",
          name: 'お知らせページ開発',
          price: '20,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: "",
          subNo: 4,
          date: "2018/12/31",
          name: '実績一覧ページ開発',
          price: '30,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: "",
          subNo: 5,
          date: "2018/12/31",
          name: '実績個別ページ開発',
          price: '20,000',
          num: 1,
          sum: 0
        },
        {
          mainNo: "",
          subNo: 6,
          date: "2018/12/31",
          name: 'お問い合わせページ開発',
          price: '35,000',
          num: 1,
          sum: 0
        },
      ],
      subtotal: 0,
      taxRatio: 1.08,
      tax: 0,
      total: 0
    }
  },

  mounted () {
    vm = this
    let editable = document.getElementsByClassName('editable')

    document.getElementsByClassName('total')[0].addEventListener(('click'), () => {
      console.log(vm.object)
    })
    document.getElementsByClassName('addItem')[0].addEventListener(('click'), () => {
      console.log("clicked ADD")
      const newData =
        {
          mainNo: "9",
          subNo: 9,
          date: "2018/12/31",
          name: 'sample',
          price: 1,
          num: 1,
          sum: 0
        }
      console.table(newData)
      const index = this.object.length
      console.log("object length is " + this.object.length)
      vm.$set(this.object, index, newData)
      vm.getDatas()
    })
    document.getElementsByClassName('deleteItem')[0].addEventListener(('click'), () => {
      console.log("clicked Delete")
      const index = this.object.length
      // vm.$delete(this.object, index)
      vm.object.splice(index-1, 1)
      console.log("delete target object length is " + this.object.length)
      vm.getDatas()
    })
    vm.getDatas()

    const el = document.getElementById('sortable')  
    const sortable = Sortable.create(el,{
      animation: 150,
      onEnd: ()=> {
        console.log("end dragging")
        editable = document.getElementsByClassName('editable')
        for(let i=0 ; i < editable.length ; i++){
          editable[i].addEventListener(('click'), ()=>{
            editable[i].contentEditable = "true"
            console.log(i+ " : " + editable[i].contentEditable)
          })
        }
      }
    })
    
    for(let i=0 ; i < editable.length ; i++){
      editable[i].addEventListener(('click'), ()=>{
        editable[i].contentEditable = "true"
        console.log(i+ " : " + editable[i].contentEditable)
      })
    }
    for(let i=0 ; i < editable.length ; i++){
      editable[i].addEventListener(('mousemove'), ()=>{
        editable[i].contentEditable = "false"
        console.log(i+ " : " + editable[i].contentEditable)
      })
    }
  },

  methods: {
    getDatas: ()=>{
      console.log("各数値を更新します")
      let sum = 0

      let price
      let num
      for(const i in vm.object){
        vm.object[i].sum = vm.removeLetter(vm.object[i].price) * vm.removeLetter(vm.object[i].num)
        sum += vm.removeLetter(vm.object[i].sum)
        vm.object[i].sum = vm.object[i].sum.toLocaleString()
      }
      vm.subtotal = sum.toLocaleString()          // add camma to subtotal
      const subs = vm.removeLetter(vm.subtotal)      // shrink subtotal
      vm.tax = Math.floor(subs * vm.taxRatio - subs) // calc tax
      vm.tax = vm.tax.toLocaleString()                // add camma to tax
      vm.total = (vm.removeLetter(subs) + vm.removeLetter(vm.tax)).toLocaleString() //calc total
    },
    createDataBase:(dbName)=>{
      const openReq = indexedDB.open(dbName)
      openReq.onupgradeneeded = (event) =>{
        console.log('db upgrade')
        db = event.target.result
        db.createObjectStore('storeName', {keyPath : 'id'})
      }
      openReq.onsuccess = (event)=>{
        console.log('database open success')
        const db = event.target.result
        console.log("db version is "+ db.version)
        db.close()
      }
      openReq.onerror = (event)=>{
        console.log('db open failed with error')
      }
    },

    deleteDataBase:(dbName)=>{
      const deleteReq = indexedDB.deleteDatabase(dbName)
      deleteReq.onsuccess = (event)=>{
        console.log('db delete success')
      }
      deleteReq.onerror = (event)=>{
        console.log('db delete failed with error')
      }
    },

    insertData:(dbName, id, name)=>{
      const data = {id : id, name: name}
      const openReq = indexedDB.open(dbName)
      openReq.onsucssess = (event)=>{
        const db = event.target.result
        const trnas = db.transaction(storeName, 'readwrite')
        const store = trans.objectStore(storeName)
        const purReq = store.put(data)
      }

    },

    removeLetter: (txt) => {
      if(isNaN(txt)){
        let replaced = txt.replace(/[^0-9]/g, '')
        return Number(replaced)
      }
      return Number(txt)
    },

    AndAddComma: (num) => {
      return num.toLocaleString()
    },

    //数字入力欄のフォーカス解除時発火
    onBlur: (e, i, param) => {
      vm.object[i][param] = e.target.innerText
      if (param === 'num' || param === 'price') {
        let sum = 0

        vm.object[i][param] = vm.removeLetter(vm.object[i][param]).toLocaleString()//異物を撮ってからComma追加
        e.target.innerText = vm.object[i][param]
        vm.object[i]['sum'] = vm.removeLetter(vm.object[i]['num']) * vm.removeLetter(vm.object[i]['price'])
        vm.object[i]['sum'] = Number(vm.object[i]['sum'])
        // calcurate subtotal with price by num
        for (const i in vm.object) {
          //console.log("[285]sum is : " + (vm.object[i].sum))
          sum += vm.removeLetter(vm.object[i].sum)
          vm.object[i].sum = vm.object[i].sum.toLocaleString()
          console.log("[287]added sum is  " + vm.removeLetter(sum))
        }
        console.log("-------")
        vm.subtotal = sum.toLocaleString()
        const subs = vm.removeLetter(vm.subtotal)
        console.log("subs: "+subs)
        vm.tax = Math.floor(subs * vm.taxRatio - subs)
        vm.tax = vm.tax.toLocaleString()
        vm.total = (vm.removeLetter(subs) + vm.removeLetter(vm.tax)).toLocaleString()
      }
    },
  }
}

</script>

<style lang="stylus">

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
    grid-template-columns .8fr .8fr 1.5fr 5fr 1fr .8fr 1fr
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
      grid-column 1 / 4
      background-color #333
      color #fff
      font-weight bold
    .payItem
      grid-column 4 / 5
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
      font-size 1.4vw
      line-height 1.6vw
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
      grid-column 5 / 7
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
