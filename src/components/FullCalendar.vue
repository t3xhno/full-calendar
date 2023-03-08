<script setup lang="ts">
import {
  EventInput,
  DateSelectArg,
  EventClickArg,
  CalendarOptions,
} from "@fullcalendar/core";
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";
import timeGridPlugin from "@fullcalendar/timegrid";
import scrollPlugin from "@fullcalendar/scrollgrid";
import multiMonthPlugin from "@fullcalendar/multimonth";
import interactionPlugin from "@fullcalendar/interaction";

/**
 * Unique ID generator
 */
const genId = (function*() {
  let id = 0;
  while (true) yield id++;
})();

const dayHandler = (e: DateSelectArg) => {
  const title = prompt("Please enter a new title for your event");
  const calendarApi = e.view.calendar;
  if (title) calendarApi.addEvent({
    id: String(genId.next().value),
    title,
    start: e.startStr,
    end: e.endStr,
    allDay: e.allDay,
    backgroundColor: "blue",
    whatever: "lol",
    thisShould: "go to extended",
    extendedProps: {
      theseAre: "also extended, but explicitly",
    },
  });
};
const eventHandler = (e: EventClickArg) => {
  console.log(e.event.title, e.event.startStr, e.event.endStr, e.event.extendedProps);
};

const calendarOptions: CalendarOptions = {
  plugins: [dayGridPlugin, interactionPlugin, scrollPlugin, timeGridPlugin, multiMonthPlugin],
  initialView: "dayGridMonth",
  select: dayHandler,
  eventClick: eventHandler,
  editable: true,
  eventResizableFromStart: true,
  dragScroll: true,
  selectable: true,
  // selectMirror: true,
  snapDuration: 1000,
  eventColor: "red",
  displayEventTime: true,
  eventTimeFormat: {
    hour: "numeric",
    minute: "2-digit",
    omitZeroMinute: true,
    meridiem: "narrow",
  },
  themeSystem: "bootstrap5",
  events: [
    { title: "Lol", date: "2023-03-07", startEditable: true, backgroundColor: "green", description: "roflmaololi" },
    { title: "Event 2", date: "2023-03-07", hello: "rofl" },
    { title: "Event 3", date: "2023-03-08" },
  ] as EventInput[],
};
</script>

<template>
  <FullCalendar id="full-cal" :options="calendarOptions">
    <template #eventContent="arg">
      <b>{{ arg.timeText }}</b>
      <i>{{ arg.event.title }}</i>
    </template>
  </FullCalendar>
</template>

<style scoped lang="scss" src="./FullCalendar.scss" />
