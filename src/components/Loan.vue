<template>
  <div>
    <b-row>
      <b-col :lg="6">
        <b-card>
          <b-form @submit="onSubmit" @reset="onReset" v-if="show">
            <b-form-group
              id="input-group-1"
              label="Enter Loan Amount:"
              label-for="input-1"
              description="The loan amount should be more than 1000 INR"
            >
              <b-form-input
                id="input-1"
                v-model="form.amount"
                placeholder="INR"
                required
              ></b-form-input>
            </b-form-group>
            <b-form-group
              id="input-group-1"
              label="Enter Loan Term:"
              label-for="input-1"
              description="The loan term should be greater than 0"
            >
              <b-form-input
                id="input-1"
                v-model="form.term"
                placeholder="Enter Number of Years"
                required
              ></b-form-input>
            </b-form-group>

            <b-button @click="approval()" v-b-modal.my-modal type="submit" variant="primary">Confirm</b-button>
          </b-form>
        </b-card>
        <b-card class="mt-3" header="My Loans">
          <pre class="m-0">{{ storedData }}</pre>
        </b-card>
        <b-modal id="my-modal" hide-header hide-header-close>Your Weekly Repayment Amount is INR {{ repayment }}
          <template #modal-ok>Send for Approval</template>
          <template #modal-cancel>Go Back</template>
        </b-modal>
      </b-col>
      <b-col :lg="6">
        <h4>Admin</h4>
        <b-card>
          <b-btn v-b-modal.approval-modal v-if="showAdmin">Approve Loan</b-btn>
        </b-card>
        <b-modal id="approval-modal" hide-header hide-header-close>Your Loan has been Approved!
          <template #modal-ok>Repay</template>
          <template #modal-cancel>Go Back</template>
        </b-modal>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  data () {
    return {
      form: {
        amount: null,
        term: null
      },
      storedData: {
        amount: [],
        term: [],
        approval_status: []
      },
      show: true,
      showAdmin: false
    }
  },
  methods: {
    onSubmit (event) {
      event.preventDefault()
      this.storedData.amount.push(this.form.amount)
      this.storedData.term.push(this.form.term)
    },
    onReset(event) {
      event.preventDefault()
      // Reset our form values
      this.form.amount = 0
      this.form.term = 0
      this.show = false
      this.$nextTick(() => {
        this.show = true
      })
    },
    approval () {
      this.storedData.approval_status.push('Sent for Approval!')
      this.showAdmin = true
    }
  },
  computed: {
    repayment () {
      return Math.round(this.form.amount/(this.form.term * 52))
    }
  }
}
</script>