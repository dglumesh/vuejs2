<template>
  <div>
    <div class="well">
      <div class="row">
        <div class="col-md-3">
          <strong>Student name:</strong>
        </div>
        <div class="col-md-3">
          {{ owner.FirstName }}
        </div>
      </div>
      <div class="row">
        <div class="col-md-3">
          <strong>Date of birth:</strong>
        </div>
        <div class="col-md-3">
          {{ owner.DOB }}
        </div>
      </div>
</div>
</div>
</template>
<script>
import OwnerService from '@/api-services/owner.service'
export default {
  name: 'OwnerDetails',
  data () {
    return {
      owner: {}
    }
  },
  created () {
    OwnerService.get(this.$router.currentRoute.params.id).then((response) => {
      this.owner = response.data
    })
  }
}
</script>
