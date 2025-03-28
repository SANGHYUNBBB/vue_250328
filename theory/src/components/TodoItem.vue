<script>
export default {
  name: 'TodoItem',
  data() {
    return {}
  },
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  emit: ['toggle-completed'],
  methods: {
    toggleCompleted() {
      this$emit('toggle-completed', this.todo.id)
    },
  },
}
</script>

<template>
  <!-- 할일 목록 -->

  <!-- <li class="completed">
    <input type="checkbox" />
    <span>입력된 리스트1</span>
    <time>2025-03-26</time>
    <i class="fa fa-trash"></i>
  </li> -->
  <li :class="{ completed: todo.completed }" @click="toggleCompleted">
    <input type="checkbox" />
    <span>{{ todo.text }}</span>
    <time>{{ todo.createAt }}</time>
    <i class="fa fa-trash" @click.stop></i>
  </li>
</template>

<style scoped>
.todo-list {
  margin: var(--space-l) auto !important;
}
.todo-list li {
  display: flex;
  align-items: center;
  gap: var(--space-s);
  border-bottom: 1px solid var(--gray200);
}
/* .todo-list li.completed {
  opacity: 0.3;
  text-decoration: line-through;
} */

.todo-list li.completed span {
  text-decoration: line-through;
}
.todo-list li > * {
  display: flex;
  align-items: center;
  gap: var(--space-s);
  padding: var(--space-s);
  cursor: pointer;
  transition: 0.3s;
}
.todo-list li:hover {
  background-color: var(--gray300);
}

.todo-list span {
  flex: 1;
}
.todo-list time {
  font-size: 0.75rem;
}
.todo-list i {
  border: 1px solid transparent;
  padding: var(--space-s);
  color: var(--gray300);
}
.todo-list i:hover {
  border: 1px solid var(--gray300);
  color: var(--danger);
}
/* 가상 요소로 사용 할 때만 제한적으로 사용!!!! */
.todo-list button::after {
  font-family: 'Font Awesome 6 Free';
  font-weight: bold;
  content: '\f793';
}
</style>
