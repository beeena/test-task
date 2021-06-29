<template>
  <div class="task-card" :class="task.id">
    <div class="card-header">
      <span class="delete-btn" @click="handleClick(task.id)" v-if="showBtn"
        >Delete</span
      >
      <span class="dots" @click="showBtn = !showBtn">...</span>
    </div>
    <div class="task-card-body">
      {{ task.id }}
      <div class="img-wrapper"></div>
      <div class="task-details">
        <div class="task-status" :class="getStatus(task.status)">
          {{ task.status }}
        </div>
        <p class="left-days">5 day left</p>
        <div class="hours">
          {{ task.hours }} hrs <span class="sep">|</span>
          <span class="price"> ${{ task.price }}</span>
        </div>
      </div>
    </div>
    <hr class="card-sep" />
    <div class="card-task-footer">
      <span class="view-order">View order</span>
      <div class="right-content">
        <div class="progress-bar" v-if="task.progress">
          <span :style="{ width: `${(task.progress / 60) * 100}%` }"></span>
        </div>
        <div class="avatar"></div>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component({
  name: "Card",
})
export default class Card extends Vue {
  @Prop() private task!: any;
  @Prop() private handleRemoveTask!: any;
  @Prop() private item!: any;

  showBtn = false;

  getStatus(status: any): any {
    return status.split(" ").join("-");
  }

  handleClick(cardID: any): any {
    this.$emit("handleRemoveTask", this.item.id, cardID);
    this.showBtn = !this.showBtn;
  }
}
</script>

<style scoped lang="scss">
.task-card {
  background-color: #fff;
  border-radius: 5px;
  margin: 0.8rem 0;

  .card-header {
    position: relative;
    display: flex;
    justify-content: flex-end;
    align-items: center;
    padding-right: 1rem;

    .delete-btn {
      position: absolute;
      background: #060606;
      right: 0;
      padding: 0.4rem 1rem;
      top: 0;
      border-radius: 6px;
      cursor: pointer;
      color: #fff;
      z-index: 11;
      font-size: 14px;
      transition: all 0.5s ease-in-out;
    }

    .dots {
      font-size: 1rem;
      font-weight: 700;
      cursor: pointer;
    }
  }
  .task-card-body {
    display: flex;
    justify-content: space-between;
    align-items: flex-start;
    padding: 1rem;

    .img-wrapper {
      width: 40px;
      height: 40px;
      background-color: #e7e7e7;
      border-radius: 5px;
    }
    .task-details {
      text-align: end;
      .task-status {
        border-radius: 2rem;
        font-size: 0.7rem;
        line-height: 0.7rem;
        font-weight: 700;
        text-transform: uppercase;
        padding: 0.4rem 1rem;
        letter-spacing: 0.02rem;
        color: #0000009e;

        &.new-order {
          background-color: rgb(231, 206, 188);
        }
        &.in-progress {
          background-color: rgb(209, 214, 224);
        }
        &.delivered {
          background-color: rgb(221, 195, 220);
        }
        &.completed {
          background-color: rgb(182, 201, 178);
        }
      }
      .left-days {
        font-size: 0.9rem;
        line-height: 0.7rem;
        color: #545050de;
      }
      .hours,
      .price {
        font-size: 0.9rem;
        line-height: 0.7rem;
        color: #545050de;
      }
      .sep {
        padding: 0 5px;
        color: #dcd1d1;
      }
      .price {
        font-weight: 700;
      }
    }
  }
  .card-sep {
    border-color: #ffffff5e;
    margin: 0;
  }
  .card-task-footer {
    padding: 1rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
    .view-order {
      font-size: 0.98rem;
      font-weight: 700;
      color: rgb(165, 158, 158);
      text-transform: capitalize;
    }
    .right-content {
      display: flex;
      align-items: center;

      .progress-bar {
        width: 60px;
        height: 0.5rem;
        background: #e7e7e7;
        border-radius: 6px;
        margin-right: 1rem;
        position: relative;

        span {
          position: absolute;
          top: 0;
          left: 0;
          background: rgb(23, 95, 23);
          height: 100%;
          border-radius: 6px;
        }
      }
      .avatar {
        width: 30px;
        height: 30px;
        border-radius: 15px;
        background-color: #eee;
      }
    }
  }
}
</style>
