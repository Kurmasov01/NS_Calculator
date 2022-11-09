<template>
    <Page>
        <ActionBar>
            <Label text="Calculator"/>
        </ActionBar>
        <StackLayout>
            <Label :text="value"></Label>
            <Label :text="result"></Label>
            <FlexboxLayout class="buttons">         
                <FlexboxLayout class="numbers" flexWrap="wrap" >
                    <Button v-for="i in 9" @tap="addNumber(i)" :key="i" class="number">{{i}}</Button>
                    <Button class="number" @tap="addOperation(operations[5])">.</Button>
                    <Button class="number" @tap="addNumber(0)">0</Button>
                    <Button class="number" @tap="calculation()">=</Button>
                </FlexboxLayout>
                <FlexboxLayout flexDirection="column" class="operations">
                    <Button class="opButton" @tap="clean()">C</Button>
                    <Button class="opButton" @tap="addOperation(operations[0])">^</Button>
                    <Button class="opButton" @tap="addOperation(operations[1])">*</Button>
                    <Button class="opButton" @tap="addOperation(operations[2])">/</Button>
                    <Button class="opButton" @tap="addOperation(operations[3])">+</Button>
                    <Button class="opButton" @tap="addOperation(operations[4])">-</Button>
                </FlexboxLayout>
            </FlexboxLayout>
        </StackLayout>
    </Page>
</template>


<script>
  export default {
    data () {
      return {
        value: "0",
        result: 0,
        operations: ["^","*", "/", "+", "-","."],
      };
    },
    methods: {
      addNumber(n) {
        if(this.value == "0")
        {
          this.value = n
        }
        else
        {
          this.value += String(n)
        }
      },
      addOperation(x) {
        if (!this.operations.includes(this.value[this.value.length - 1])) 
        {
          this.value += String(x)
        }
      },
      calculation() 
        {
          try
          {
            if((this.result = eval(this.value.replace(/\^/, "**" ))) == "Infinity")
            {
              this.result = "На ноль делить нельзя"
            }
          }
          catch(error)
          {
            this.result = "Ошибка"
          }

        },
      clean() {
        this.value = "0"
        this.result = 0
      }
    }
  };
</script>


<style scoped>
    Label {
        font-size: 32;
        text-align: right;
        background: #fff;
        color: #111;
        padding: 20;
    }
    Button {
        margin: 0;
        border-radius: 1%;
        font-size: 25;
    }
  
    .number {
        width: 33.3333333%;
    }
    .operations {
        width: 50%;
    }
    .opButton {
        background-color: rgb(44, 206, 255);
        margin: 0;
        height: 16.75%;
    }
</style>
