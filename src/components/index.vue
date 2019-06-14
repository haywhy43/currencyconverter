<template>
    <div id="index">
        <div><h1>Currency Converter</h1></div>     
        <div class="main">
            <div class="main-inner">
                <div class="inputs">
                    <h3>From</h3>
                    <div class="from-inputs mb-3">
                        <div class="input-group input-group-lg big">
                            <input type="text" class="form-control" placeholder="Enter Amount" v-model="amount">
                        </div><br>
                        <div class="input-group input-group-lg small">
                            <input type="text" class="form-control" placeholder="Currency" v-model="from">
                        </div>
                    </div>
                    <h3>To</h3>
                    <div class="from-inputs">
                        <div class="input-group input-group-lg small">
                            <input type="text" class="form-control" placeholder="Currency"  v-model="to">
                        </div><br>
                        <div class="input-group input-group-lg big">
                            <input type="text" class="form-control" placeholder="" disabled v-model="result">
                        </div>
                    </div><br>
                </div>
                <div class="btndiv">
                    <button class="btn btn-primary" v-on:click="convert">Convert</button>
                </div>
            </div>
        </div>   
    </div>
</template>

<script>
export default {
    name: 'Index',
    data() {
        return{
            from: '',
            to: '',
            amount: '',
            result: ''
            
        
        }
    },
    methods: {
        onToChange: (e) =>{
        },
        convert: function(){
            const to = this.to;
            const from = this.from;
            const amount = this.amount;
            fetch(`https://api.exchangeratesapi.io/latest?base=${from}`)
            .then(response => response.json())
            .then(data => {
                const rates = data.rates;
                const figure = rates[`${to}`];
                console.log(amount * figure)
                this.result = amount * figure
            })
        }
    }
}
</script>

<style scoped>
    @import url('https://fonts.googleapis.com/css?family=Lobster&display=swap');
    #index{
        font-family: 'Lobster', cursive;
    }

    h1{
        
        font-size: 30px;
        color: rgb(216, 207, 207);
        padding: 15px;
        padding-left: 50px;
        letter-spacing: 3px;
    }

    .main{
        height: 80vh;
        display: flex;
        justify-content: center;
        align-items: center

        
    }
    .main-inner{
        background-color: #eee;
        height: 20em;
        border-radius: 10px;
        padding-left: 4rem;
        padding-right: 4rem;
        padding-bottom: 1rem;
        padding-top: 2rem;
        box-shadow: 0px 30px 60px rgba(0, 0, 0, 1);
    }

    .inputs{
        display: flex; 
        flex-direction: column;
        align-items: center;
    }

    .form-control{
        background-color:transparent;
        border-color: rgb(124, 115, 115);
        font-size: 15px;
    }

    .from-inputs{
        display: flex;
        justify-content: space-between;
    }
    .big{
        width: 80%;
    }
    .small{
        width: 20%
    }
    .btndiv{
        display: flex;
        justify-content: center;
    }
    .btn-primary{
        background: #0f0c29;
        background: -webkit-linear-gradient(to right, #24243e, #302b63, #0f0c29);
        background: linear-gradient(to right, #24243e, #302b63, #0f0c29); 
        border-color: transparent; 
        color: rgb(124, 115, 115)!important;
    }

    .btn-primary:hover{
        background: transparent;
        border-color: #0f0c29;
        color: #0f0c29!important;
    }

    

    .btn{
        width: 60%;
        color: #eee!important;
        transition:0.3s
    }


    @media screen and (max-width: 1024px){
        .main-inner{
            width: 65%
        }
    }

    @media screen and (max-width: 414px){
        .main-inner{
            width: 80%;
            padding: 2em;
        }

        .big{
            width: 70%;
        }

        .small{
            width: 30%;
        }

        .form-control{
            font-size: 10px;
        }

        h1{
            padding: 0;
            text-align: center;
        }
    }
</style>

