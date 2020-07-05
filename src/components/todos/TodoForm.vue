<template>

  <div id="todo-form">

    <form @submit.prevent="handleSubmit">
      <label>Todo</label>
      <input 
        type="text"
        :class="{ 'has-error': submitting && invalidName }"
        v-model="todo.name"
        @focus="clearStatus"
        @keypress="clearStatus"
      />

      <p v-if="error && submitting" class="error-message">
        ❗This Field can't be empty
      </p>
      <p v-if="success" class="success-message">
        ✅ Todo successfully added
      </p>

      <button>Add Todo</button>
    </form>

  </div>

</template>

<script>
  export default {
    name: 'todo-form',
    data() {
      return {
        submitting: false,
        error: false,
        success: false,
        todo: {
          name: ''
        },
      }
    },
    methods: {
      handleSubmit() {
        this.submitting = true
        this.clearStatus()

        if (this.invalidName) {
          this.error = true
          return
        }

        this.$emit('add:todo', this.todo)
        this.todo = {
          name: ''
        }
        this.error = false
        this.success = true
        this.submitting = false
      },

      clearStatus() {
        this.success = false
        this.error = false
      }
    },
    computed: {
      invalidName() {
        return this.todo.name === ''
      }
    }
  }
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>
