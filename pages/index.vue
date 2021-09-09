<template>
  <v-container class="text-center" >
    <!-- <v-row justify="center" align="center">
      <v-col cols="12" sm="8" md="6"> -->
        <v-card flat min-width="832">
          <v-card-text class="headline py-12">
            <p class="text-center black--text font-weight-bold">Tech Challenge - Calculator</p>
          </v-card-text>
          <v-card-actions class="pb-10">
            <v-spacer></v-spacer>
            <CalculatorUI />
            <v-spacer></v-spacer>
          </v-card-actions>
        </v-card>
      <!-- </v-col>
    </v-row> -->
  </v-container>
</template>

<script>

  import CalculatorUI from '~/components/calculator'

  export default {
    name: 'Calculator',
    components: { CalculatorUI }
  }
</script>

<style lang="scss" scoped>

</style>