<template>
  <div class="container">
    <div id="background-sketch"></div>
    <div class="content">
      <div class="title-component">
        <h1 class="title">{{ title }}</h1>
        <p class="subtitle">{{ phrase }}</p>
      </div>

      <div class="learn-more-component">
        <p>Conocer más</p>
        <hr>
      </div>

      <div class="calendar-view-container">
        <CalendarView :dateText="eventDates" :monthText="eventMonth"></CalendarView>
      </div>
    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import CalendarView from '~/components/CalendarView.vue'
import * as tecnoXData from "../static/data.json";

const createSkecth = () => {
  let run = Pts.quickStart('#background-sketch', '#F1F3F4')
  run( (time, ftime) => {
    // get a line from pointer to center, and use it for direction and magnitude calculations
  // console.log('space.center', space.center)
    const spaceCenter = new Pt([300, space.height - 150])
    let ln = space.pointer.$subtract(spaceCenter.$add(0.1) );
    let dir = ln.$unit();
    let mag = ln.magnitude();
    let mag2 = space.size.magnitude();

    // create a grid of lines
    let lines = Pts.Create.gridPts( space.innerBound, 20, 10 ).map( (p) => {
      let dist = p.$subtract( spaceCenter ).magnitude() / mag2;
      return new Pts.Group(p, p.$add( dir.$multiply( dist*(20 + mag/5) ) )) 
    });
    
    // form.strokeOnly("#fe3").line( [space.center, space.pointer] );
    form.strokeOnly("#2A7886").lines( lines );
  });
}

export default {
  components: {
    Logo,
    CalendarView
  },
  setup() {
    const eventDates = tecnoXData.event_dates
    const eventMonth = tecnoXData.event_month
    const title = tecnoXData.title
    const phrase = tecnoXData.phrase

    return {
      eventDates, eventMonth, title, phrase
    }
  },
  mounted: () => {
    if(!process.server) {
      createSkecth()
    }
  }
}
</script>

<style lang="stylus">
@import '../assets/theme.styl'

.container {
  // margin: 0 auto;
  // min-height: 100vh;
  // display: flex;
  // justify-content: center;
  // align-items: center;
  // text-align: center;
  
}
.content {
  position: relative;
  min-height: 100vh;
  margin: 0 auto;
  pointer-events: none;
}

#background-sketch{
  width: 100%;
  height: 100%;
  position: absolute;
  top: 0;
  left: 0;
}

.title-component {
  max-width: 400px;
  position: absolute;
  bottom: 100px;
  left: 50px;
  text-align: left;
}

.title {
  display: block;
  font-weight: 300;
  font-size: 100px;
  letter-spacing: 1px;
  color: black;
}

.subtitle {
  font-weight: 300;
  word-spacing: 5px;
  padding-bottom: 15px;
  font-size: 24px;
  line-height: 31px;
  color: gray;
}

.learn-more-component{
  position: absolute;
  bottom: 32px;
  left: 50%;
  transform: translateX(-50%);
  text-decoration: line-through;
  pointer-events: initial;
  cursor pointer
}
.learn-more-component > hr {
  border: 1px solid color2;
}
.learn-more-component:hover {
  color: color2;
}

.calendar-view-container {
  position: absolute;
  top: 40px;
  right: 50px;
  pointer-events: initial;
}

@media screen and (max-width: 600px) {
  .title {
    font-size: 48px
  }
  .subtitle {
    font-size: 18px;
  }
  .title-component {
    bottom: 80px;
    left: 20px;
  }
}

</style>
