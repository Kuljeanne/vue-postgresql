<template>
  <table>
    <caption>Список пользователей</caption>
    <tr>
      <th>Имя</th>
      <th>Фамилия</th>
      <th></th>
    </tr>
    <tr v-if="users.length === 0">
      <td colspan="3">Список пользователей пуст, заполните форму выше</td>
    </tr>
    <tr v-else v-for="user  in users" :key="user.id">
      <td>{{ user.name }}</td>
      <td>{{ user.surname }}</td>
      <td>
        <div class="edit-btns">
          <button @click="$emit('edit', user)" class="table-btn">
            <IconEdit />
          </button>
          <button @click="$emit('remove', user)" class="btn table-btn">
            <IconDelete />
          </button>
        </div>
      </td>
    </tr>
  </table>
</template>

<script lang="ts">
import type { User } from "@/types";
import IconDelete from "./icons/IconDelete.vue";
import IconEdit from "./icons/IconEdit.vue";

export default {
  components: {
    IconDelete, IconEdit
  },
  data() {
    return {
      isEditing: true
    }
  },
  props: {
    users: {
      type: Array<User>,
      required: true
    }
  }
}

</script>

<style scoped>
table {
  border-collapse: collapse;
  border: 3px solid black;
  font-size: 2rem;
  max-width: 50%;
}

caption {
  font-size: 2.4rem;
  margin-bottom: 1rem;
}

th {
  background-color: #a299ea;
}

th,
td {
  min-width: 20rem;
  border: 1px solid black;
  padding: 5px;
  text-align: center;
}

.table-btn {
  cursor: pointer;
  border: none;
  background: transparent;
}

.edit-btns {
  display: flex;
  justify-content: space-around;
}
</style>