<template>
  <div class="card-wrapper">
    <div class="card" v-for="(item, i) in items" :key="i">
      <p class="card-state">{{ item.state }}</p>
      <Card
        v-for="(task, index) in item.tasksCard"
        :key="index"
        :task="task"
        :item="item"
        @handleRemoveTask="handleRemoveTask"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Card from "./Card.vue";

@Component({
  name: "Tasks",
  components: {
    Card,
  },
})
export default class Tasks extends Vue {
  items: any = [
    {
      id: 1,
      state: "new order",
      tasksCard: [
        { id: 1, img: "#", status: "new order", hours: "20", price: "25" },
        { id: 2, img: "#", status: "new order", hours: "20", price: "25" },
      ],
    },
    {
      id: 2,
      state: "in progress",
      tasksCard: [
        {
          id: 1,
          img: "#",
          status: "in progress",
          hours: "20",
          price: "25",
          progress: "20",
        },
      ],
    },
    {
      id: 3,
      state: "waiting for buyer",
      tasksCard: [
        {
          id: 1,
          img: "#",
          status: "delivered",
          hours: "20",
          price: "25",
          progress: "20",
        },
        {
          id: 2,
          img: "#",
          status: "delivered",
          hours: "20",
          price: "25",
          progress: "40",
        },
      ],
    },
    {
      id: 4,
      state: "completed",
      tasksCard: [
        { id: 1, img: "#", status: "completed", hours: "20", price: "25" },
        { id: 2, img: "#", status: "completed", hours: "20", price: "25" },
        { id: 3, img: "#", status: "completed", hours: "20", price: "25" },
      ],
    },
  ];

  handleRemoveTask(taskID: any, cardID: any): any {
    const columnIndex = this.items.findIndex(
      (column: any) => column.id == taskID
    );
    const cardIndex = this.items[columnIndex].tasksCard.findIndex(
      (card: any) => card.id == cardID
    );
    this.items[columnIndex].tasksCard.splice(cardIndex, 1);
  }
}
</script>

<style scoped lang="scss">
.card-wrapper {
  display: flex;
  overflow-x: auto;
  .card {
    width: 24%;
    background-color: #e7e7e7;
    margin: 0.5rem;
    border-radius: 4px;
    text-align: left;
    padding: 0.8rem;
    min-width: 240px;

    .card-state {
      font-size: 1rem;
      line-height: 1rem;
      text-transform: uppercase;
      font-weight: 600;
      color: #847f7f;
      margin-top: 0.8rem;
      letter-spacing: 0.02rem;
    }
  }
}
</style>
