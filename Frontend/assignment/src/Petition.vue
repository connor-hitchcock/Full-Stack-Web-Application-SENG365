<template>
  <div>
    <div v-if="errorFlag" style="color: red;">
      {{ error }}
    </div>

    <div v-else>
      <div id="petitions">
        <table>
          <h2>All Petitions:</h2>
          <tr v-for="petition in petitions" v-bind:key="petition">
            <td>Id:         {{ petition.petitionId }}</td>
            <td>Title:      {{ petition.title }}</td>
            <td>Category:   {{ petition.category }}</td>
            <td>Author:     {{ petition.authorName }}</td>
            <td>Signatures: {{ petition.signatureCount }}</td>
          </tr>
        </table>
      </div>
    </div>
  </div>
</template>

<script>
export default {

  data () {
    return {
      error: "",
      errorFlag: false,
      petitions: []
    }
  },

  mounted: function() {
    this.getPetitions();
  },

  methods: {

    getPetitions: function() {
      this.$http.get('http://localhost:4941/api/v1/petitions')
      .then((response) => {
        this.petitions = response.data;
      })
      .catch((error) => {
        this.errorFlag = true;
        console.error(error);
      })
    }

  }
}
</script>