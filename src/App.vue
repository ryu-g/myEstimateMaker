<template lang="pug">
#app
  h1 {{ msg }}
  .metaInfo
    .meta
      p 御見積番号 : 000000
      p 発行日 : 0000
  .information
    .direction
      p hogehogehogehoge株式会社 御中
      p 〒000-0000
      p 太陽系地球日本東京都千代田区1-1-1-1
      p 超スーパーハイパーウルトラ長い名前のビルディング40号11階
      p ご担当: 超長名字侍 名前非尋常長太郎 様
    .from
      p hogehogehogehoge株式会社
      p 〒000-0000
      p 太陽系地球日本東京都千代田区1-1-1-1
      p 超スーパーハイパーウルトラ長い名前のビルディング40号11階
      p TEL 0000-000-0000
      p FAX 0000-000-0000
      p E-mail tooLongAndSuperRangeEmailAdress@hogeMail.com
      p 担当 超長名字侍 名前非尋常長太郎
  .estimatePrice
    p 御見積り合計金額
      ul.table
        li.heading.number Main No.
        li.heading.number sub no.
        li.heading.date 年 / 月 / 日
        li.heading.name 品目名
        li.heading.price 単価
        li.heading.amout 数量
        li.heading.subtotal 金額

        li.item.number 1 
        li.item.number 1
        li.item.date 2019/12/31
        li.item.name とてもとても長い長い長いファッキンスーパーロングウルトラ品目名
        li.item.price 99,999,999,999
        li.item.amout 999
        li.item.subtotal 99999999

        li.item.number 
        li.item.number 2
        li.item.date 2019/12/31
        li.item.name とてもとても長い長い長いファッキンスーパーロングウルトラ品目名
        li.item.price 999999
        li.item.amout 999
        li.item.subtotal 99999999

        li.item.number 2 
        li.item.number 1
        li.item.date 2019/12/31
        li.item.name とてもとても長い長い長いファッキンスーパーロングウルトラ品目名
        li.item.price 999999
        li.item.amout 999
        li.item.subtotal 99999999

        li.item.number 2 
        li.item.number 1
        li.item.date 2019/12/31
        li.item.name とてもとても長い長い長いファッキンスーパーロングウルトラ品目名
        li.item.price 999999
        li.item.amout 999
        li.item.subtotal 99999999

        li.item.number 2 
        li.item.number 1
        li.item.date 2019/12/31
        li.item.name とてもとても長い長い長いファッキンスーパーロングウルトラ品目名
        li.item.price 999999
        li.item.amout 999
        li.item.subtotal 99999999

        li.item.number 2 
        li.item.number 1
        li.item.date 2019/12/31
        li.item.name とてもとても長い長い長いファッキンスーパーロングウルトラ品目名
        li.item.price 999999
        li.item.amout 999
        li.item.subtotal 99999999

        li.item.number 2 
        li.item.number 1
        li.item.date 2019/12/31
        li.item.name 短い名前
        li.item.price 5
        li.item.amout 2
        li.item.subtotal 10
        

        li.result.subAmount 小計
        li.item.subAmount -----
  
        li.result.tax 消費税
        li.item.tax -----

        li.result.total 合計
        li.item.total 999000

    p 消費税
    p 金額
  .other
   p 支払条件
   p 振込手数料負担
   p 有効期限
   p 備考欄  
</template>
<script>
export default {
  name: 'app',
  data () {
    return {
      msg: '御見積書'
    }
  }
}

</script>

<style lang="sass">
@page
  margin: 0

#app 
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
  display: block
  width: 80vw
  height: 113vw
  border: 1px solid #999
  margin: 50px auto

h1, h2 
  padding: 60px 0 40px 0
  margin: 0
  font-weight: normal
p
  font-size: 16px
  margin: 5px

ul 
  list-style-type: none
  padding: 0

li 
  display: inline-block
  margin: 0 10px

.metaInfo
  display: flex
  flex-direction: row-reverse
  width: 80%
  margin: 20px auto
  text-align: left
  p 
    font-size: 12px 
.information
  width: 80%
  margin: 20px auto
  display: flex
  text-align: left
  p
    font-size: 14px
  .direction
    width: 50%
  .from
    width: 50%
    margin-left: 20px
.estimatePrice
  width: 90%
  margin: 0 auto
  .table
    display: grid
    // Main No., sub no. 年月日,品目名,単価,数量,金額
    grid-template-columns: 65px  60px 100px 1fr 60px 40px 120px
    grid-gap: 4px 2px
    margin-bottom: 10px
    padding: 20px
    li
      margin: 0px
      padding: 8px 5px

    .heading
      background-color: #333
      color: #eee
      font-weight: bold
      font-size: 12px
      line-height: 12px
      display: flex
      align-items: center
      justify-content: center

    .item
      display: flex
      align-items: center
      justify-content: center
      background-color: #eee
      color: #333
      font-size: 12px
      line-height: 16px

    .result
      grid-column: 5 / 7
      background-color: #333
      color: #eee
      font-weight: bold
      font-size: 14px
      line-height: 14px
      display: flex
      align-items: center
      justify-content: center



</style>
