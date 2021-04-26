<template>
  <div class="container">
    <div class="calc">

    <div class="row bg-secondary">

      <div v-model="message" class="col-sm text-center border border-primary position-relative">
        <span class="write"> {{showOperator}}</span>
         {{ current || 0}}
      </div>

    </div>

    <div class="row">
      <div @click="clearAll" class="col-sm border border-primary bg-light">
        C
      </div>
      <div @click="square" class="col-sm border border-primary bg-light">
        x<sub>2</sub>
      </div>
      <div @click="percent" class="col-sm border border-primary bg-light">
        %
      </div>
      <div @click="divide" class="col-sm border border-primary bg-warning">
        /
      </div>
    </div>

    <div class="row">
      <div @click="append(7)" class="col-sm border border-primary bg-light">
        7
      </div>

      <div @click="append(8)" class="col-sm border border-primary bg-light">
        8
      </div>
      <div @click="append(9)" class="col-sm border border-primary bg-light">
        9
      </div>
      <div @click="multiple" class="col-sm border border-primary bg-warning">
        *
      </div>
    </div>

    <div class="row">
      <div @click="append(4)" class="col-sm border border-primary bg-light">
        4
      </div>

      <div @click="append(5)" class="col-sm border border-primary bg-light">
        5
      </div>
      <div @click="append(6)" class="col-sm border border-primary bg-light">
        6
      </div>
      <div @click="add" class="col-sm border border-primary bg-warning">
        +
      </div>
    </div>

      <div class="row">
        <div @click="append(1)" class="col-sm border border-primary bg-light">
          1
        </div>
        <div @click="append(2)" class="col-sm border border-primary bg-light">
          2
        </div>
        <div @click="append(3)" class="col-sm border border-primary bg-light">
          3
        </div>
        <div @click="minus" class="col-sm border border-primary bg-warning">
          -
        </div>
      </div>

      <div class="row">
        <div @click="sign" class="col-sm border border-primary bg-light">
          +-
        </div>

        <div @click="append(0)" class="col-sm border border-primary bg-light">
          0
        </div>
        <div @click="dot('.')" class="col-sm border border-primary bg-light">
          .
        </div>
        <div @click="equal" class="col-sm border border-primary bg-warning">
          =
        </div>
      </div>



   </div>

  </div>

</template>

<script>
export default {

  data () {
    return {
      current :'',
      operator : null,
      previous : null,
      operatorClicked : false,
      showOperator : ''
    }
  },
  methods : {
    clearAll(){
      this.current = '';
      this.showOperator = '';
    },
    percent (){
      this.current = parseFloat(this.current) / 100
    },
    square (){
      this.current = this.current * this.current
    },
    append(num){
      if (this.operatorClicked){
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${num}`
     // this.current = this.current num
    },
    sign(){
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`
    },
    dot(){
      if (this.current.indexOf('.') === -1){
        this.append('.')
      }
    },
    divide(){
      this.operator = (a,b) => a/b;
      this.operatorClicked = true;
      this.previous = this.current;
      this.showOperator = '/';

    },
    add(){
      this.operator = (a,b) => a+b;
      this.operatorClicked = true;
      this.previous = this.current;
      this.showOperator = '+';

    },
    multiple(){
      this.operator = (a,b) => a*b;
      this.operatorClicked = true;
      this.previous = this.current;
      this.showOperator = '*';

    },
    minus(){
      this.operator = (a,b) => a-b;
      this.operatorClicked = true;
      this.previous = this.current;
      this.showOperator = '-';

    },
    equal(){
      this.current = this.operator(parseFloat(this.previous), parseFloat(this.current))
      this.previous=null;
    },
  },
}
</script>

<style scoped>

.calc{
  font-size:  2.5rem;
  width: 50%;
  margin: 160px auto;
}
.write{
  color: red;
  font-size: 1.7rem;
  position: absolute;
  right: 2px;

}

</style>
