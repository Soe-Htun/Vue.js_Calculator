<template>
    <div class="Calculator">
        <div class="display">{{current || '0'}}</div>
        <div class="btn" @click="clear">C</div>
        <div class="btn" @click="sign">⌫</div>
        <div class="btn" @click="percent">%</div>
        <div class="operator" :style="{backgroundColor: operatorSign==='di' ? '#409EFF' : ''}" @click="Calculate('di')">÷</div>
        <div class="btn" @click="append('7')">7</div>
        <div class="btn" @click="append('8')">8</div>
        <div class="btn" @click="append('9')">9</div>
        <div class="operator" :style="{backgroundColor: operatorSign==='mul' ? '#409EFF' : ''}" @click="Calculate('mul')">*</div>
        <div class="btn" @click="append('4')">4</div>
        <div class="btn" @click="append('5')">5</div>
        <div class="btn" @click="append('6')">6</div>
        <div class="operator" :style="{backgroundColor: operatorSign==='min' ? '#409EFF' : ''}" @click="Calculate('min')">-</div>
        <div class="btn" @click="append(1)">1</div>
        <div class="btn" @click="append('2')">2</div>
        <div class="btn" @click="append('3')">3</div>
        <div class="operator" :style="{backgroundColor: operatorSign==='add' ? '#409EFF' : ''}" @click="Calculate('add')">+</div>
        <div class="btn zero" @click="append('0')">0</div>
        <div class="btn" @click="dot">.</div>
        <div class=" operator" :style="{backgroundColor: operatorSign==='equal' ? '' : ''}" @click="Calculate('equal')">=</div>
        
    </div>
</template>
<script>
export default {
    name:'Calculator',
    data() {
        return {
            operatorSign:'',
            previous:'',
            current:'',
            operator:'',
            operatorClicked:false
        }
    },
    methods:{
        clear(){
            this.current=''
        },
        sign(){
            // this.current =this.current.charAt(0) === '-'?
            // this.current.slice(1) : `-${this.current}`;
            this.current= this.current.slice(0,-1)
        },
        percent(){
            this.current = `${parseFloat(this.current)/100}`;
        },
        append(number){
            if(this.operatorClicked){
                this.current='';
                this.operatorClicked=false;
            }
            this.current= `${this.current}${number}`;
            this.number=number;
        },
        dot(){
            if(this.current.indexOf('-') === -1){
                this.append('.');
            }
        },
        setPrevious(){
            this.operatorClicked= true;
            this.previous =this.current
        },
        Calculate(operatorSign){
            this.operatorSign= operatorSign;
            if(operatorSign === 'di'){
                this.operator=(a,b)=> b / a;
                this.setPrevious();
                //this.operatorSign=operatorSign
            }else if(operatorSign === 'mul'){
                this.operator=(a,b)=>  a * b;
                this.setPrevious();
            }else if(operatorSign === 'min'){
                this.operator=(a,b)=> b - a;
                this.setPrevious();
            }else if(operatorSign === 'add'){
                this.operator=(a,b)=> a + b;
                this.setPrevious();
            }else if(operatorSign === 'equal'){
                this.current =`${this.operator(
                    parseFloat(this.current),
                    parseFloat(this.previous)
                )}`
                this.previous=''
            }
        },
        onCalc(e){
            if(e.keyCode === 97){
                if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
                }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 97){
                if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
                }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 98){
                if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
            }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 99){
                if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
                }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 100){
                  if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
                }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 101){
                if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
                }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 102){
                if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
                }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 103){
                if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
                }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 104){
                if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
                }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 105){
                if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
                }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 110 || e.keyCode ===190){
                if(this.operatorClicked){
                    this.current='';
                    this.operatorClicked=false;
                }
                this.current= `${this.current}${e.key}`
            }else if(e.keyCode === 107 ){
                this.Calculate('add');
            }else if(e.keyCode === 61 || e.keyCode===13){
                this.Calculate('equal');
            }else if(e.keyCode === 109){
                this.Calculate('min');
            }else if(e.keyCode === 106){
                this.Calculate('mul');
            }else if(e.keyCode === 111){
                this.Calculate('di');
            }else if(e.keyCode === 53){
                this.percent();
            }else if(e.keyCode === 46){
                this.clear();
            }else if(e.keyCode === 8){
                this.sign();
            }
        }
    },
    created(){
        window.addEventListener('keydown', this.onCalc)
    }
}
</script>

<style>
.Calculator{
    width: 400px;
    margin: 0 auto;
    font-size: 40px;
    display: grid;
    grid-template-columns: repeat(4,1fr);
    grid-auto-rows: minmax(50px, auto);
    background-color: #333;
}

.display{
    grid-column: 1/5;
    color: white;
    height: 60px;
}
.zero{
    text-align: center;
    grid-column: 1/3;
    background-color: rgb(122, 100, 100)(122, 100, 100);
}
.btn{
    background-color: rgb(242, 242, 242);
    border: 1px solid #999;
    height: 60px;
}
.btn:active{
    background-color: grey
}
.operator{
    background-color: orange;
    color: white;
    border: 1px solid #999;
}
@media screen and (max-width: 1024px) {
  .Calculator {
    width: 100%;
  }
}
</style>