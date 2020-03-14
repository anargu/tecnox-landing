
<template>
  <div id="calender-view">
    <div class="dates">{{ dateText }}</div>
    <div class="month">{{ monthText }}</div>
    <div class="suscribe">Inscribirse</div>
  </div>
</template>

<script>
	export default {
    props: {
      dateText: String,
      monthText: String
    },
    setup() {
      return {}
    }
  }
</script>

<style lang="stylus" scoped>
@import '../assets/theme.styl'

#calender-view
  border 2px solid color3
  border-radius 16px
  padding 18px 12px
.dates
  font-size 72px
  line-height 94px
.month
  font-size 72px
  line-height 47px
.suscribe
  padding 48px 12px 0px 12px
  font-weight bold
  cursor pointer
  text-align center
  text-decoration: line-through

#calender-view:hover
  border-color color2
.suscribe:hover
  color color2
@media screen and (max-width: 600px)
  .dates
  .month
    font-size 24px
    line-height 32px
    text-align center
  .suscribe
    padding 20px 8px 0px 8px
</style>