<template>
  <tr>
                <td>{{ owner.FirstName }}</td>
                <td>{{ owner.MiddleName }}</td>
                <td>{{ owner.LastName }}</td>
                 <td>{{ owner.Mobile }}</td>
                  <td>{{ owner.Telephone }}</td>
                   <td>{{ owner.Email }}</td>
                    <td>{{ owner.Address }}</td>
                     <td>{{ owner.DOB }}</td>
                     <td>{{ owner.NIC }}</td>
    <td>
      <b-button variant="default"
      @click="onDetailsClick">Details</b-button>
    </td>
    <td>
      <b-button variant="success"
      @click="onUpdateClick">Update</b-button>
    </td>
    <td>
      <b-button variant="danger"
      @click="onDeleteClick">Delete</b-button>
    </td>
  </tr>
</template>
<script>
export default {
  name: 'OwnerListRow',
  props: [ 'owner' ],
  methods: {
    onDetailsClick () {
      this.$emit('details', this.owner.StudentID)
    },
    onUpdateClick () {
      this.$emit('update', this.owner.StudentID)
    },
    onDeleteClick () {
      this.$emit('delete', this.owner.StudentID)
    }
  }
}
</script>
