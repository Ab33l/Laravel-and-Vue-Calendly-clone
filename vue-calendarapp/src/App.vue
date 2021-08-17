<template>
  <div id="app">
    <header>
      Schedule an Event
    </header>
    <div class="main" :class="$mq">
      <div class="calendar-holder">
        <calendar :events="events" />
      </div>
      <div class="form-holder">
        <h3>Schedule an event</h3>
        <event-form />
      </div>
    </div>
    <footer>
      Copyrights Reserved © 2021 | Comitium Pvt. Ltd.
    </footer>
  </div>
</template>

<script>
import Vue from 'vue';
import Calendar from './components/Calendar.vue'
import EventForm from './components/EventForm.vue'
import Pusher from 'pusher-js';
import VueMq from 'vue-mq';
Vue.use(VueMq, {
  breakpoints: {
    sm: 620,
    md: 850,
    lg: Infinity,
  }
})
export default {
  name: 'app',
  components: {
    Calendar,
    EventForm
  },
  data(){
    return {
      events: [{
        title     :  'event1',
        start     : '2018-07-09',
        cssClass  : 'blue',
        YOUR_DATA : {}
      },
      {
        title     : 'event2',
        start     : '2018-07-18',
        end       : '2018-07-13',
        cssClass  : ['orange']
      },
      {
        title     : 'event3',
        start     : '2021-08-19',
        end       : '2021-08-21',
        cssClass  : ['red']
      },
      {
        title     :  'event4',
        start     : '2021-08-03',
        cssClass  : 'blue',
        YOUR_DATA : {}
      },
      {
        title     : 'event5',
        start     : '2021-10-1',
        end       : '2021-10-20',
        cssClass  : ['red']
      },
      ]
    }
  },
  created(){
    // Add your pusher credentials
    const pusher = new Pusher('PUSHER_KEY', {
      cluster: 'PUSHER_CLUSTER',
      encrypted: true,
    });
    const channel = pusher.subscribe('schedule');
    channel.bind('new-event', (data) => {
      this.events = [
        ...this.events,
        data
      ]
    })
  }
}
</script>

<style>
body{
  background-color: whitesmoke;
}
*{
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  outline: none;
  color: #2c3e50;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
header{
  top: 0;
  color: rgb(60, 60, 60);
  text-align: left;
  padding: 1rem 4rem;
  font-size: 2rem;
  background-color: rgb(244, 244, 244);
  box-shadow: 0 1px 10px rgba(0, 0, 0, 0.1);
}
/* desktops */
.main.lg {
  display: flex;
  align-items: flex-start;
  padding: 1rem 4.8rem;
  margin-top: 2rem;
}
.main.lg .calendar-holder {
  width: 60%;
  position: sticky;
  top: 1rem;
  margin-right: 1.6rem;
}
.main.lg .form-holder {
  padding: 1rem;
  width: 40%;
  margin-left: 1.6rem;
}
/* tablet */
.main.md {
  display: flex;
  align-items: flex-start;
  padding: 1rem;
}
.main.md .calendar-holder {
  width: 55%;
  position: sticky;
  top: 1rem;
  margin-right: 1.6rem;
}
.main.md .form-holder {
  width: 45%;
  margin-left: 1.6rem;
}
/* mobiles */
.main.sm {
  display: flex;
  align-items: center;
  justify-content: center;
  flex-wrap: wrap-reverse;
  padding: 1rem 2rem;
}
.main.sm .calendar-holder {
  width: 100%;
  top: 0;
}
.main.sm .form-holder {
  width: 100%;
}
.form-holder h3,
.form-holder h4 {
  text-align: left;
}



footer{
  margin-top: 2rem;
  margin-bottom: 1rem;
}
</style>