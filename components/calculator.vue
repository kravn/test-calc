<template>
  <v-card
    light flat
    width="800"
    class="pa-0">
    <v-card class="calc-screen pa-3 ma-1" outlined>
      <v-card-actions class="pa-0">
        <v-spacer></v-spacer>
        <div v-if="answer">
          Ans = <strong>{{ answer }}</strong>
        </div>
        <div v-else>&nbsp;</div>
      </v-card-actions>
      <v-card-actions class="pa-0">
        <v-spacer></v-spacer>
        <div class="display-1">
          {{ strValue }}
        </div>
      </v-card-actions>
    </v-card>
    <template 
      v-for="(n, key) in calcBtns">
      <div
        v-if="n.active"
        @click="collect(n.key, n.multi)"
        :key="key"
        :class="`btn--calculator ${n.color}`"
        v-html="n.label">
      </div>
      <div
        v-else
        :key="key"
        :class="`btn--calculator ${n.color}`"
        v-html="n.label">
      </div>
    </template>
  </v-card>
</template>

<script>

  import { CALCULATOR_BUTTONS } from '~/components/constants/calculator.js'
  import Calcu from '@mroutput/jscalc'

  const btns = { CALCULATOR_BUTTONS }

  export default {
    name: 'Calculator',
    computed: {
      calcBtns () {
        return btns.CALCULATOR_BUTTONS
      }
    },
    methods: {
      collect (val, multi = false) {
        var c = new Calcu()

        if (this.strValue === 0 || this.strValue === '0') {
          this.strValue = ''
        }

        if (multi) {
          if (val === '=') {
            try {
              this.answer = c.exec(this.strValue)
            }
            catch(e) {
              this.answer = e
            }
          }
          else if (val === 'ce') {
            this.strValue = '0'
            this.answer = null
          } else {
            this.flag = false
            this.strValue += `${val}`
          }
        }
        else {
          if (!this.flag) {
            this.strValue += `${val}`
            this.flag = true
          }
          
        }
                
      }
    },
    data() {
      return {
        strValue: '0',
        answer: null,
        flag: false
      }
    }
  }
</script>