<template>
  <full-calendar :events="events" />
</template>

<script>
import FullCalendar from 'vue-fullcalendar';
export default {
  name: 'Calendar',
  props: ['events'],
  components: {
    FullCalendar
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
.title{
  font-family: inherit !important;
  font-weight: 800;
  font-size: 1.2rem;
}
.comp-full-calendar {
  background-color: rgba(0,0,0,0) !important;
}
.week{
  text-transform: uppercase;
  color: grey;
}
.weeks, .week, .week-row, .day-cell{
  border: none !important;
  min-height: 60px !important;
  display: flex;
  align-items: flex-end;
  justify-content: center;
}
.weeks, .week{
  align-items: center !important;
}
.events-day, .event-box{
  min-height: 60px !important;
  display: flex;
  align-items: stretch;
  justify-content: center;
}
.event-box{
  align-items: flex-end !important;
}
.events-day{
  position: relative;
}
.event-box{
  width: 100%;
  position: absolute;
}
/* red */
.event-item.red {
  background: rgb(235, 77, 77, 0.1) !important;
  border-top: 2px solid rgb(235, 77, 77);
  border-bottom: 2px solid rgb(235, 77, 77);
}
.event-item.is-start.red {
  border-left: 2px solid rgb(235, 77, 77);
}
.event-item.is-end.red {
  border-right: 2px solid rgb(235, 77, 77);
}
/* blue */
.event-item.blue {
  background: rgb(59, 59, 163, 0.1) !important;
  border-top: 2px solid rgb(59, 59, 163);
  border-bottom: 2px solid rgb(59, 59, 163);
}
.event-item.is-start.blue {
  border-left: 2px solid rgb(59, 59, 163);
}
.event-item.is-end.blue {
  border-right: 2px solid rgb(59, 59, 163);
}
/* orange */
.event-item.orange {
  background: rgba(255, 166, 0, 0.1) !important;
  border-top: 2px solid rgba(255, 166, 0);
  border-bottom: 2px solid rgba(255, 166, 0);

}
.event-item.is-start.orange {
  border-left: 2px solid rgba(255, 166, 0);
}
.event-item.is-end.orange {
  border-right: 2px solid rgba(255, 166, 0);
}
/* green */
.event-item.green {
  background: rgb(49, 155, 49, 0.1) !important;
  border-top: 2px solid rgb(49, 155, 49);
  border-bottom: 2px solid rgb(49, 155, 49);
}
.event-item.is-start.green{
  border-left: 2px solid rgb(49, 155, 49);
}
.event-item.is-end.green{
  border-right: 2px solid rgb(49, 155, 49);
}
.blue,
.orange,
.red,
.green {
  font-size: 13px;
  font-weight: 500;
  text-transform: capitalize;
}
.event-item {
  padding: 2px 0 2px 4px !important;
  min-height: 56px;
  margin-right: 0 !important;
  margin-left: 0 !important;
  width: 100%;
  color: rgb(91, 91, 91) !important;
  line-height: 1.8rem !important;
}
.event-item.is-start {
  border-radius: 16px 0 0 16px !important;
}
.event-item.is-end {
  border-radius: 0 16px 16px 0 !important;
}
.event-item.is-start.is-end {
  border-radius: 16px !important;
}
</style>