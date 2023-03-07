<script setup lang="ts">
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";
import scrollPlugin from "@fullcalendar/scrollgrid";
import interactionPlugin from "@fullcalendar/interaction";

const dayHandler = (e) => console.log("Clicked on day: ", e);
const eventHandler = (e) => console.log("Clicked on event: ", e);

const calendarOptions = {
  plugins: [dayGridPlugin, interactionPlugin, scrollPlugin],
  initialView: "dayGridMonth",
  dateClick: dayHandler,
  eventClick: eventHandler,
  editable: true,
  eventColor: "red",
  events: [
    { title: "Lol", date: "2023-03-07", startEditable: true, backgroundColor: "green", description: "roflmaololi" },
    { title: "Event 2", date: "2023-03-07" },
    { title: "Event 3", date: "2023-03-08" },
  ],
};
</script>

<template>
  <FullCalendar id="full-cal" :options="calendarOptions">
    <template #eventContent="arg">
      {{ arg.event.title }}
    </template>
  </FullCalendar>
</template>

<style scoped lang="scss" src="./FullCalendar.scss" />
