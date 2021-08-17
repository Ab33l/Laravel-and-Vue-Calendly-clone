<template>
  <form @submit.prevent="handleSubmit">
    <div class="input-holder">
      <input type="text" v-model="event.title" required />
      <label>Event title</label>
    </div>
    <div class="input-holder">
      <date-picker v-model="event.start" required /> 
      <label :class="{labelValid: !!event.start}">Start date</label>
    </div>
    <div class="input-holder">
      <date-picker :placeholder="'End date'" v-model="event.end" required /> 
      <label :class="{labelValid: !!event.end}">End date</label>
    </div>
    <div class="input-holder">
      <textarea v-model="event.data.description" required></textarea>
      <label>Event description</label>
    </div>
    <div class="input-holder">
      <color-picker @colorPicked="selectColor" :color="event.cssClass" />
    </div>
    <div class="input-holder">
      <button type="submit">Schedule</button>
    </div>
  </form>
</template>


<script>
import DatePicker from 'vuejs-datepicker';
import format from 'date-fns/format';
import ColorPicker from './ColorPicker';
export default {
  name: 'EventForm',
  data(){
    return {
      event: {
        title: '',
        start: '',
        end: '',
        cssClass: '',
        data: {
          description: ''
        }
      }
    }
  },
  methods: {
    async handleSubmit(){
      const start = format(this.event.start, 'YYYY-MM-DD');
      const end = format(this.event.end, 'YYYY-MM-DD');
      const event = {
        ...this.event,
        start,
        end
      }
      console.log(event);
      const req = await fetch('http://localhost:4001/schedule', {
        method: 'POST',
        body: JSON.stringify(event),
        headers: {
          'content-type': 'application/json'
        }
      });
      await req.json();
      this.resetValues();
    },
    selectColor(color){
      this.event = {
        ...this.event,
        cssClass: color
      }
    },
    resetValues(){
      this.event = {
        title: '',
        start: '',
        end: '',
        cssClass: '',
        data: {
          description: ''
        }
      }
    }
  },
  components: {
    DatePicker,
    ColorPicker
  }
}
</script>


<style>
form{
  display: flex;
  flex-direction: column;
  align-items: stretch;
  font-size: 1rem;
  font-weight: 500;
}
form *{
  transition: all 0.3s ease;
}
form .input-holder{
  display: flex;
  align-items: flex-start;
  width: 100%;
  margin: 1.4rem 0;
}
form .input-holder label{
  position: absolute;
  pointer-events: none;
  margin: 0.6rem auto;
}
form .input-holder input,
form .input-holder textarea{
  padding: 0.6rem 0;
  background-color: rgba(0,0,0,0);
  border: none;
  border-bottom: 0.12rem solid rgba(0,0,0,0.8);
  font-size: 1rem;
  font-weight: 500;
}
form .input-holder textarea{
  resize: vertical;
  min-height: 4.8rem;
  max-height: 100vh;
}

form .input-holder input:valid + label,
form .input-holder input:focus + label,
form .input-holder textarea:valid + label,
form .input-holder textarea:focus + label,
.labelValid{
  transform: translate(0, -1.4rem);
  color: grey;
  font-size: 12px;
}
form .input-holder input,
form .input-holder textarea,
form .input-holder .vdp-datepicker,
form .input-holder .vdp-datepicker div input{
  width: 100%;
}
form .input-holder button{
  padding: 0.4rem 2rem;
  border: 0.12rem solid rgba(0,0,0,0);
  color: whitesmoke;
  border-radius: 2px;
  font-size: 1.2rem;
  cursor: pointer;
  margin-right: 0;
  width: 100%;
  background-color: rgba(0,0,0,0.6);
}
form .input-holder button:hover{
  border: 0.12rem solid rgba(0,0,0,0.8);
  color: whitesmoke;
}
</style>