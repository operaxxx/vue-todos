<template>
  <div>
    <Card style="width:600px;margin:auto">
      <p slot="title" style="text-align:left">
        <Icon type="ios-paper" />待办事项
      </p>
      <a href="#" slot="extra" @click.prevent="openAddModal">
        <Icon type="md-add" />
      </a>
      <ul class="todo_ul">
        <template></template>
        <todoItem
          v-for="(todo,index) in todoList"
          :key="todo.id"
          :index="index"
          @remove="remove(index)"
          :todo="todo"
        >
          <template v-slot:todoContent="contentProps">
            <span
              :style="{fontSize : '18px', textDecoration : contentProps.isChecked ? 'line-through' : ''}"
            >{{todo.content}}</span>
          </template>
        </todoItem>
      </ul>
    </Card>

    <Modal v-model="addTodoModal" :mask-closable="false" @on-ok="addTodo" @on-cancel="addCancle">
      <Input v-model="newTodoText" placeholder="请输入待办事项..." style="width:300px" />
    </Modal>
  </div>
</template>

<script>
import todoItem from "../components/TodoItem.vue";
import iView from "../../node_modules/iview";

export default {
  components: {
    todoItem,
    iView
  },
  data() {
    return {
      todoList: [
        { id: 1, content: "洗衣服" },
        { id: 2, content: "理发" },
        { id: 3, content: "跑步" }
      ],
      todoNextId: 4,
      addTodoModal: false,
      newTodoText: ""
    };
  },
  methods: {
    addTodo: function() {
      if (!this.newTodoText) {
        this.$Message.warning("请输入待办事项");
        return;
      }

      this.todoList.push({
        id: this.todoNextId++,
        content: this.newTodoText
      });

      this.newTodoText = "";
      this.$Message.info("添加成功");
    },
    remove: function(index) {
      this.todoList.splice(index, 1);
      this.$Message.info("移除");
    },
    openAddModal: function() {
      this.addTodoModal = true;
    },
    addCancle: function() {
      this.newTodoText = "";
    }
  }
};
</script>

<style scoped>
.card {
  width: 600px;
  margin: auto;
}

.todo_ul {
  text-align: left;
  padding-left: 5px;
  list-style-type: none;
}
</style>
