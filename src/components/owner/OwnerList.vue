<template>
  <div>
   <div>
    <b-row>
      <b-col
        md="2"
        offset-md="10">
        <router-link :to="{ name: 'OwnerCreate' }">Create owner</router-link>
      </b-col>
    </b-row>
    <br>
    <b-row>
      <b-col md="12">
        <div class="table-responsive">
          <table class="table table-striped">
            <thead>
              <tr>

                <th>First Name</th>
                <th>Middle Name</th>
                <th>Last Name</th>
                <th>Mobile</th>
                <th>Telephone</th>
                <th>Email</th>
                <th>Address</th>
                <th>DOB</th>
                <th>NIC</th>
              </tr>
            </thead>
            <tbody>
             <owner-list-row
                v-for="owner in owners"
                :key="owner.id"
                :owner="owner"
                @details="detailsOwner"
                @update="updateOwner"
                @delete="deleteOwner"
                />
            </tbody>
          </table>
        </div>
      </b-col>
    </b-row>
    <b-modal
      ref="deleteConfirmModal"
      title="Confirm your action"
      @ok="onDeleteConfirm"
      @hide="onDeleteModalHide">
      <p class="my-4">Are you sure you want to delete this owner?</p>
    </b-modal>

    <b-modal
      ref="alertModal"
      :title="alertModalTitle"
      :ok-only="true">
      <p class="my-4">{{ alertModalContent }}</p>
    </b-modal>
  </div>
  </div>
</template>
<script>
import OwnerService from '@/api-services/owner.service'
import OwnerListRow from '@/components/owner/OwnerListRow'
export default {
  name: 'OwnerList',
  components: {
    OwnerListRow
  },
  data () {
    return {
      owners: [],
      selectedOwnerId: null,
      alertModalTitle: '',
      alertModalContent: ''
    }
  },
  created () {
    // OwnerService.getAll().then((response) => {
    //   this.owners = response.data
    // })
    this.fetchOwners()
  },
  methods: {
    detailsOwner (StudentID) {
      this.$router.push({ name: 'OwnerDetails', params: { id: StudentID } })
    },
    updateOwner (StudentID) {
      this.$router.push({ name: 'OwnerUpdate', params: { id: StudentID } })
    },
    deleteOwner (StudentID) {
      this.selectedOwnerId = StudentID
      this.$refs.deleteConfirmModal.show()
    },
    fetchOwners () {
      OwnerService.getAll().then((response) => {
        this.owners = response.data
      })
    },
    onDeleteConfirm () {
      OwnerService.delete(this.selectedOwnerId).then(() => {
        this.alertModalTitle = 'Successfully'
        this.alertModalContent = 'Successfully deleted Account Owner'
        this.$refs.alertModal.show()
        this.fetchOwners()
      }).catch((error) => {
        this.alertModalTitle = 'Error'
        this.alertModalContent = error.response.data
        this.$refs.alertModal.show()
      })
    },
    onDeleteModalHide () {
      this.selectedOwnerId = null
    }
  }
}
</script>
