<template lang="pug">
#app
  h1 {{ msg }}
  .metaInfo
    .meta
      p 御見積番号 : 000000
      p 発行日 : 0000
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
      li {{from.phone}}
      li {{from.fax}}
      li {{from.Email}}
      li {{from.person}}
  
  .estimatePrice
    ul.table
      li.payHeading 御見積り金額
      li.payItem {{ total }} 円
    ul.table
      li.heading.number Main No.
      li.heading.number sub no.
      li.heading.date 年 / 月 / 日
      li.heading.name 品目名
      li.heading.price 単価
      li.heading.amout 数量
      li.heading.subtotal 金額

    div#hogehoge
      ul.table(v-for = "(value, key) in object")
        li.item.number(contenteditable='true' @blur="onBlur($event, key, 'mainNo')") {{ value.mainNo }} 
        li.item.number(contenteditable='true' @blur="onBlur($event, key, 'subNo')") {{ value.subNo }}
        li.item.date(contenteditable='true' @blur="onBlur($event, key, 'date')") {{ value.date }}
        li.item.name(contenteditable='true' @blur="onBlur($event, key, 'name')") {{ value.name }}
        li.item.price(contenteditable='true' @blur="onBlur($event, key, 'price')") {{ value.price }}
        li.item.amout(contenteditable='true' @blur="onBlur($event, key, 'num')") {{ value.num }}
        li.item.subtotal(contenteditable='false' @blur="onBlur($event, key, 'sum')") {{ value.sum }}


      
    ul.table
      li.result.subAmount 小計
      li.item.subAmount {{ subtotal }}

      li.result.tax 消費税(8%)
      li.item.tax {{ tax }}

      li.result.total 合計
      li.item.total {{ total }}

    p 消費税
    p 金額
  .other
   p 支払条件
   p 振込手数料負担
   p 有効期限
   p 備考欄  
</template>

<script>
import 'normalize.css';
let vm
export default {
  name: 'app',
  data () {
    return {
      msg: '御見積書',
      direction: {
        company: "hogehogehogehoge株式会社 御中",
        postalCode: "000-0000",
        address1: "太陽系地球日本東京都千代田区1-1-1-1",
        address2: "超スーパーハイパーウルトラ長い名前のビルディング40号11階",
        person: "ご担当: 超長名字侍 名前非尋常長太郎 様"
      },
      from: {
        company: "hogehogehogehoge株式会社 御中",
        postalCode: "000-0000",
        address1: "太陽系地球日本東京都千代田区1-1-1-1",
        address2: "超スーパーハイパーウルトラ長い名前のビルディング40号11階",
        phone: "TEL:000-000-000",
        fax: "FAX:000-000-000",
        Email: "E-mail tooLongAndSuperRangeEmailAdress@hogeMail.com",
        person: "担当: 超長名字侍 名前非尋常長太郎 様"
      },
      object: [
        {
          mainNo: 1,
          subNo: 1,
          date: 30,
          name: 'itemName',
          price: 0,
          num: 1,
          sum: 0
        },
        {
          mainNo: 1,
          subNo: 1,
          date: 30,
          name: 'itemName',
          price: 0,
          num: 1,
          sum: 0
        },
        {
          mainNo: 1,
          subNo: 1,
          date: 30,
          name: 'itemName',
          price: 0,
          num: 1,
          sum: 0
        },
        {
          mainNo: 2,
          subNo: 1,
          date: 30,
          name: 'itemName',
          price: 0,
          num: 1,
          sum: 0
        }
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
      console.log(vm)
    })
  },
  methods: {
    onBlur: (e, i, param) => {
      vm.object[i][param] = e.target.innerText
      if (param === 'num'||param === 'price') {
        let sum = 0

        vm.object[i][param] = Number(vm.object[i][param].replace(/[^0-9]/g, ''))
        e.target.innerText = vm.object[i][param]
        vm.object[i]['sum'] = (vm.object[i]['num']) * vm.object[i]['price']
        // calcurate subtotal with price by num
        for (const i in vm.object) {
          sum += Number(vm.object[i].sum)
        }

        vm.subtotal = sum
        vm.tax = Math.floor(vm.subtotal * vm.taxRatio - vm.subtotal)
        vm.total = vm.subtotal + vm.tax   
      }
    }
  }
}

</script>

<style lang="stylus">
@page
  margin 0

#app 
  font-family 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  display block
  width 80vw
  height 113vw
  border 1px solid #999
  margin 50px auto

  h1
    font-size 3vw
    font-weight normal
    padding 6vw 0 4vw 0
    margin 0

  font-size 1.4vw
  margin 5px

ul 
  list-style-type none
  padding 0
  margin 0


.metaInfo
  display flex
  flex-direction row-reverse
  width 80%
  margin 20px auto
  text-align left
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
      font-size 1.4vw
      line-height: 2.5vw
  .from
    width 50%
    margin-left 20px
    li
      font-size 1.4vw
      line-height: 2.5vw

.estimatePrice
  width 90%
  margin 5vw auto
  .table
    display grid
    // Main No., sub no. 年月日,品目名,単価,数量,金額
    grid-template-columns 1fr 1fr 1.5fr 5fr 1fr 1fr 1fr
    grid-gap 4px 2px
    margin 2px 0
    li
      margin 0
      padding .8vw .5vw
      font-size 1.4vw

    .payHeading
      grid-column 1 / 4
      background-color #333
      color #fff
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
      color #333
      font-size 1.2vw
      line-height 1.6vw

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



</style>
