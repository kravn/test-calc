<template>
  <v-card
    light flat
    width="800"
    class="pa-0">
    <v-card class="calc-screen pa-3 ma-1" outlined>
      <v-card-actions class="pa-0">
        <v-spacer></v-spacer>
        
        <div v-if="answer || show">
          <transition name="bounce"  enter-active-class="animated tada" leave-active-class="animated bounceOutRight">
            <div v-show="show">
              Ans = <strong>{{ answer }}</strong>
            </div>
          </transition>
        </div>
        
        <div v-else>&nbsp;</div>
      </v-card-actions>
      <v-card-actions class="pa-0">
        <v-spacer></v-spacer>
        
        <transition name="slide-fade">
          <div v-show="show" class="display-1">
          {{ strValue }}
          </div>
        </transition>
        
      </v-card-actions>
    </v-card>
    
    <div class="calc-keys">
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
    </div>
    
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
            this.reset = true
            this.show = false
            try {
              this.answer = c.exec(this.strValue)
            }
            catch(e) {
              this.answer = e
            }
            setTimeout(() => {
              this.show = true
            }, 100);
          }
          else if (val === 'ce') {
            this.resetValue()
          } else {
            if (this.reset) {
              this.strValue = ''
              this.reset = false
            }
            this.flag = false
            this.strValue += `${val}`
          }
        }
        else {
          if (!this.flag) {
            this.strValue += `${val}`
            this.flag = true
          } else {
            this.strValue = this.strValue.slice(0, -1)
            this.strValue += `${val}`
          }
          
        }
                
      },
      resetValue () {
        this.strValue = '0'
        this.answer = null
      }
    },
    watch: {
      reset (val) {
        if (val) {
          // this.resetValue()
        }
      }
    },
    data() {
      return {
        strValue: '0',
        answer: null,
        flag: false,
        show: true,
        reset: false
      }
    }
  }
</script>