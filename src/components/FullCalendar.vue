<script setup lang="ts">
import { ref } from "vue";
import FullCalendar from "@fullcalendar/vue3";
import dayGridPlugin from "@fullcalendar/daygrid";
import scrollPlugin from "@fullcalendar/scrollgrid";
import interactionPlugin from "@fullcalendar/interaction";

const genId = (function*() {
  let id = 0;
  while (true) {
    yield id++;
    if (id >= 100) id = 0;
  };
})();

/**
 * Needs further typing
 */
interface EventObject {
  extendedProps: Record<string, unknown>;
  title: string;
};

const calendar = ref<typeof FullCalendar | null>(null);

const dayHandler = (e) => {
  const title = prompt("Please enter a new title for your event");
  if (calendar.value) {
    const calendarApi = calendar.value.getApi();
    calendarApi.addEvent({
      id: String(genId.next().value),
      title,
      start: e.dateStr,
      end: e.dateStr,
      allDay: e.allDay,
      backgroundColor: "blue",
    });
  };
};
const eventHandler = (e) => {
  const eventObj: EventObject = e.event;
  console.log(eventObj.extendedProps, eventObj.title);
};

const calendarOptions = {
  plugins: [dayGridPlugin, interactionPlugin, scrollPlugin],
  initialView: "dayGridMonth",
  dateClick: dayHandler,
  eventClick: eventHandler,
  editable: true,
  eventColor: "red",
  events: [
    { title: "Lol", date: "2023-03-07", startEditable: true, backgroundColor: "green", description: "roflmaololi" },
    { title: "Event 2", date: "2023-03-07", hello: "rofl" },
    { title: "Event 3", date: "2023-03-08" },
  ],
};
</script>

<template>
  <FullCalendar ref="calendar" id="full-cal" :options="calendarOptions">
    <template #eventContent="arg">
      {{ arg.event.title }}
    </template>
  </FullCalendar>
</template>

<style scoped lang="scss" src="./FullCalendar.scss" />
