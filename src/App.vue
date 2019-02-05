<template lang="pug">
#app
  .metaInfo
    .meta
      p 御見積番号 : 000000
      p 発行日 : 0000
  h1 {{ msg }}
  .information
    ul.direction
      li {{ direction.company }}
      li 〒 {{ direction.postalCode }}
      li {{ direction.address1 }}
      li {{ direction.address2 }}
      li {{ direction.person }}
    ul.from
      li {{from.company}}
      li 〒 {{from.postalCode}}
      li {{from.address1}}
      li {{from.address2}}
      li TEL : {{from.phone}}
      li {{from.fax}}
      li MAIL : {{from.Email}}
      li 担当 : {{from.person}}
  
  .estimatePrice
    ul.table
      li.payHeading 御見積り金額
      li.payItem {{ total }} 円
    ul.table
      li.heading.number Main No.
      li.heading.number sub no.
      li.heading.date 年 / 月 / 日
      li.heading.name 品目名
      li.heading 単価
      li.heading 数量
      li.heading 金額

    div#hogehoge
      ul.table(v-for = "(value, key) in object")
        li.item.number.editable(contenteditable='true' @blur="onBlur($event, key, 'mainNo')") {{ value.mainNo }} 
        li.item.number.editable(contenteditable='true' @blur="onBlur($event, key, 'subNo')") {{ value.subNo }}
        li.item.date.editable(contenteditable='true' @blur="onBlur($event, key, 'date')") {{ value.date }}
        li.item.name.editable(contenteditable='true' @blur="onBlur($event, key, 'name')") {{ value.name }}
        li.item.price.editable(contenteditable='true' @blur="onBlur($event, key, 'price')") {{ value.price }}
        li.item.amount.editable(contenteditable='true' @blur="onBlur($event, key, 'num')") {{ value.num }}
        li.item.subtotal(contenteditable='false' @blur="onBlur($event, key, 'sum')") {{ value.sum }}

    ul.table
      li.addItem 末尾に追加
      li.deleteItem 末尾を削除
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
let vm
export default {
  name: 'app',
  data () {
    return {
      msg: '御見積書',
      direction: {
        company: "beidp 御中",
        postalCode: "",
        address1: "",
        address2: "",
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
              company: "ヒゲダルマ株式会社",
              postalCode: "000-0000",
              address1: "東京都千代田区1-1-1",
              address2: "クソながファッキンロングネーミングビルディング101",
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
    document.getElementsByClassName('total')[0].addEventListener(('click'), () => {
      console.log(vm.object)
    })
    document.getElementsByClassName('addItem')[0].addEventListener(('click'), () => {
      console.log("clicked ADD")
      const newData = 
        {
          mainNo: "999",
          subNo: "999",
          date: "2036/21/26",
          name: 'sample',
          price: 0,
          num: 999,
          sum: 99
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
heading-bg = #333
item-bg = #efefef
uneditableItem-bg = #dedede



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
    padding 2vw 0 6vw 0
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
      background-color item-bg
      font-weight bold
      
    .heading
      background-color heading-bg
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
      background-color item-bg
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
      background-color: uneditableItem-bg

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
    
</style>
