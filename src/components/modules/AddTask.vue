<template>
  <article class="addTask">
    <section class="addTask__wrapper">
      <label class="addTask__label" for="addTask">
        <input
          ref="addTask__input"
          id="addTask"
          class="addTask__input"
          type="text"
          placeholder="Add a task"
          v-model="newTask"
          @keydown.enter="addTask()" />
      </label>
    </section>
  </article>
</template>

<script>
import { mapActions } from 'vuex';

export default {
  name: 'addTask',
  props: ['listID'],
  data() {
    return {
      newTask: null,
    };
  },
  mounted() {
    const ele = this.$refs.addTask__input;
    ele.focus();
  },
  methods: {
    ...mapActions([
      'addNewTask',
    ]),
    addTask() {
      const task = {
        listID: this.listID,
        newTask: {
          id: new Date().valueOf(),
          title: this.newTask,
          completed: false,
        },
      };
      this.addNewTask(task);
      this.newTask = '';
    },
  },
};
</script>

<style lang="scss" scoped>
.addTask {
  &__wrapper {
    display: flex;
    flex-flow: row nowrap;
    justify-content: space-between;
    align-items: center;

    padding: 1rem 0;
  }

  &__label {
    flex: 1 1 100%;
  }

  &__input {
    width: 100%;
    border: 0 none;
    background: transparent;
    outline: 0 none;
  }

  &__btn {
    font-size: 1.2rem;
    flex: 1 0 11rem;
  }
}
</style>
