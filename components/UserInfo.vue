
<template>
  <b-container fluid>
    <b-row class="my-1" v-for="type in types" :key="type.type">
      <b-col sm="3">
        <label :for="`type-${type.type}`">{{ type.name }}:</label>
      </b-col>
      <b-col sm="9">
        <b-form-input :id="`type-${type.type}`" :type="type.type"></b-form-input>
      </b-col>
    </b-row>
  </b-container>
</template>

<script>
  export default {
    data() {
      return {
        types: [
          {
            type: 'text',
            name: 'Full Name'
          },
          {
            type: 'number',
            name: 'Phone #'
          },
          {
            type: 'date',
            name: 'Birthdate'
          }
        ]
      }
    }
  }
</script>

<style scoped>

</style>
