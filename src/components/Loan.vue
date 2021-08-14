<template>
  <div>
    <b-card>
      <b-form @submit="onSubmit" @reset="onReset" v-if="show">
        <b-form-group>
          <b-form-input
            label="Amount Required:"
            id="input-1"
            v-model="form.amount"
            type="number"
            placeholder="Enter Amount Required"
            required
          ></b-form-input>
          <b-form-input
            label="Loan Term"
            id="input-1"
            v-model="form.term"
            type="number"
            placeholder="Enter Loan Term"
            required
          ></b-form-input>
        </b-form-group>

        <b-button type="submit" variant="primary">Repay</b-button>
      </b-form>
    </b-card>
    <b-card class="mt-3" header="List of Loans">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

<script>
  export default {
    data() {
      return {
        form: {
          amount: 0,
          term: 0
        },
        show: true
      }
    },
    methods: {
      onSubmit(event) {
        event.preventDefault()
        alert(JSON.stringify(this.form))
      },
      onReset(event) {
        event.preventDefault()
        // Reset our form values
        this.form.email = ''
        this.form.name = ''
        this.form.food = null
        this.form.checked = []
        // Trick to reset/clear native browser form validation state
        this.show = false
        this.$nextTick(() => {
          this.show = true
        })
      }
    }
  }
</script>