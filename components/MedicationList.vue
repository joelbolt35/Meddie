<template>
  <div>
    <b-button id="newMedButton" v-b-modal.my-modal>+ Add New Medication</b-button>

    <!-- The modal -->
    <b-modal
      id="my-modal"
      ref="modal"
      title="Add Your Medication"
      @show="resetModal"
      @hidden="resetModal"
      @ok="handleOk"
    >
      <form ref="form" @submit.stop.prevent="handleSubmit">
        <!-- Drug -->
        <b-form-group
          :state="drugState"
          label="Drug"
          label-for="drug-input"
          invalid-feedback="Drug is required"
        >
          <b-form-input
            id="drug-input"
            placeholder="Drug name"
            v-model="drug"
            :state="drugState"
            list="my-list-id"
            required
          ></b-form-input>
          <h4>Recommendations:</h4>
          <ul>
            <li v-for="(rxterm, index) in rxterms" :key="`${index}`">{{ rxterm }}</li>
          </ul>
        </b-form-group>

        <!-- Strength -->
        <b-form-group
          :state="strengthState"
          label="Strength"
          label-for="strength-input"
          invalid-feedback="Strength is required"
        >
          <b-form-input
            id="strength-input"
            placeholder="Strength list"
            v-model="strength"
            :state="strengthState"
            required
          ></b-form-input>
        </b-form-group>
      </form>
    </b-modal>

    <!-- Test Output -->
    <div class="mt-3">
      Submitted Drugs:
      <div v-if="medications.length === 0">--</div>
      <ul v-else class="mb-0 pl-3">
        <li
          v-for="medication in medications"
          :key="medication.drug"
          :id="medication.drug"
        >{{ medication }}</li>
      </ul>
    </div>
    <!-- End Test Output -->

    <!-- <Medication v-for="medication in medications" :key="medication.drug" :id="medication.drug" :medication="medication" /> -->
  </div>
</template>

<script>
import Medication from "~/components/Medication";
import axios from "axios"
export default {
  components: {
    Medication
  },
  data() {
    return {
      drug: "",
      strength: "",
      drugState: null,
      strengthState: null,
      medications: [],
      rxterms: []
    };
  },

  watch: {
    drug: async function() {
      if (this.drug.length == 0) {
        this.rxterms = [];
        return;
      };

      try {
        const response = await axios.get(`https://clinicaltables.nlm.nih.gov/api/rxterms/v3/search?terms=${this.drug}`);
        this.rxterms = response.data[1]
        console.log(response.data[1]);
      } catch (error) {
        console.error(error);
      }
    }
  },

  methods: {
    // This checks to see if the whole form is valid
    checkFormState() {
      const valid = this.$refs.form.checkValidity();
      this.drugState = this.drug !== "" ? "valid" : "invalid";
      this.strengthState = this.strength !== "" ? "valid" : "invalid";
      return valid;
    },

    //Clears the modal fields
    resetModal() {
      this.drug = "";
      this.strength = "";
      this.drugState = null;
      this.strengthState = null;
    },

    //Submit event
    handleOk(bvModalEvt) {
      // Prevent modal from closing
      bvModalEvt.preventDefault();
      // Trigger submit handler
      this.handleSubmit();
    },

    handleSubmit() {
      // Exit when the form isn't valid
      if (!this.checkFormState()) {
        return;
      }
      // Push the Medications information

      this.medications.push(this.drug);
      this.medications.push(this.strength);
      // Hide the modal manually
      this.$nextTick(() => {
        this.$refs.modal.hide();
      });
    }
  }
};
</script>

<style>
#newMedButton {
  margin-left: 15px;
  margin-top: 10px;
}
</style>
