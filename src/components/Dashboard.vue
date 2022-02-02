<template>
  <v-container>

    <!-- Form Starts -->
    <v-form>
      <v-row class="text-center mt-4">
        <v-col cols="12" sm="12" md="4">
            <v-text-field
              v-model="description"
              label="Description"
              counter="25"
              hint="Describe Your Transaction"
              solo
            ></v-text-field>
        </v-col>
        <v-col cols="12" sm="12" md="4">
            <v-text-field
              v-model="amount"
              type="number"
              label="Add Amount"
              solo
            ></v-text-field>
        </v-col>
        <v-col cols="12" sm="12" md="4">
          <v-select
            :items="typeOfTransactions"
            label="Choose Type Of Transaction"
            solo
            v-model="transaction"
          ></v-select>
        </v-col>
      </v-row>
    </v-form>
    <!-- Form Ends -->
    
    <!-- Add Transaction Button Starts -->
    <v-row>
      <v-col md="9" sm="12"></v-col>
      <v-col md="3" sm="12">
          <v-btn
            color="success"
            elevation="6"
            x-large
            @click="handleInput"
          > ADD TRANSACTION
          </v-btn>
      </v-col>
    </v-row>
    <!-- Add Transaction Button Ends -->

    <v-row class="mt-8"><v-divider inset></v-divider></v-row>
    
    <!-- Lists Begin -->
    <v-row class="text-center mt-4">

      <!-- Income List -->
      <v-col cols="12" sm="12" md="4">
        <v-card
          class="mx-auto"
          max-width="300"
          tile
        >
        <v-list shaped>
        <v-subheader class='success'>YOUR INCOMES</v-subheader>
        <v-list-item-group
          v-model="selectedItem"
          color="primary"
        >
          <v-list-item
            v-for="(item, i) in incomeItems"
            :key="i"
          >
            <v-list-item-content>
              <v-list-item-title v-text="item.desc"></v-list-item-title>
              <v-list-item-subtitle>Rs. {{item.amt}}</v-list-item-subtitle>
            </v-list-item-content>

            <v-list-item-action>
                <v-btn icon @click="handleTransactionDelete(i, 'income')"> 
                    <v-icon color="grey">mdi-trash-can</v-icon>
                </v-btn>
            </v-list-item-action>
            
          </v-list-item>
        </v-list-item-group>
      </v-list>
      </v-card>
      </v-col>

      <!-- Balance Display -->
      <v-col cols="12" sm="12" md="4" class="balance">
          Current Balance: {{this.currBal}}
      </v-col>

      <!-- Expense List -->
      <v-col cols="12" sm="12" md="4">
        <v-card
          class="mx-auto"
          max-width="300"
          tile
        >
        <v-list shaped>
        <v-subheader class='error'>YOUR EXPENSES</v-subheader>
        <v-list-item-group
          v-model="selectedItem"
          color="primary"
        >
          <v-list-item
            v-for="(item, i) in expenseItems"
            :key="i"
          >
            <v-list-item-content>
              <v-list-item-title v-text="item.desc"></v-list-item-title>
              <v-list-item-subtitle>Rs. {{item.amt}}</v-list-item-subtitle>
            </v-list-item-content>

            <v-list-item-action>
                <v-btn icon @click="handleTransactionDelete(i, 'expense')"> 
                    <v-icon color="grey">mdi-trash-can</v-icon>
                </v-btn>
            </v-list-item-action>
          </v-list-item>
        </v-list-item-group>
      </v-list>
      </v-card>
      </v-col>

    </v-row>
    
  </v-container>
</template>

<script>
  export default {
    name: 'Dashboard',
    mounted(){
      if(localStorage.incomeItems){
        this.incomeItems = JSON.parse(localStorage.incomeItems);
      }
      if(localStorage.expenseItems){
        this.expenseItems = JSON.parse(localStorage.expenseItems);
      }
      if(localStorage.currBal){
        this.currBal = JSON.parse(localStorage.currBal);
      }
    },
    watch : {
      incomeItems(newIncomeItems) {
        localStorage.incomeItems = JSON.stringify(newIncomeItems);
      },
      expenseItems(newExpenseItems){
        localStorage.expenseItems = JSON.stringify(newExpenseItems);
      },
      currBal(newCurrBal){
        localStorage.currBal = JSON.stringify(newCurrBal);
      }
    },
    methods: {
      handleInput(){
        this.amount =Number(this.amount)
        if(this.transaction == 'Income'){
          this.incomeItems.unshift({desc:this.description, amt:this.amount, type:this.transaction})
          this.currBal += this.amount
          localStorage.setItem("incomeItems",this.incomeItems)
        }else{
          this.expenseItems.unshift({desc:this.description, amt:this.amount, type:this.transaction})
          this.currBal -= this.amount
        }

        this.description = this.amount = this.transaction = ""
      },

      handleTransactionDelete(i, trans){
        if(trans=='income'){
          var amt1 = this.incomeItems[i].amt
          this.incomeItems.splice(i, 1);
          this.currBal -= amt1
        }else{
          var amt2 = this.expenseItems[i].amt
          this.expenseItems.splice(i, 1);
          this.currBal += amt2
        }
      }
    },
  
    data: () => ({
      description: '',
      amount : '',
      transaction : '',
      typeOfTransactions : ['Income', 'Expense'],
      selectedItem: 0,
      incomeItems : [],
      expenseItems : [],
      currBal : 0,
    }),
  }
</script>

<style scoped>
  .balance{
    font-family: "Lucida Sans Unicode", "Lucida Grande", sans-serif;
    font-size: 37px;
    letter-spacing: 0px;
    word-spacing: -5px;
    color: #000000;
    font-weight: 700;
    text-decoration: none;
    font-style: normal;
    font-variant: small-caps;
    text-transform: uppercase;
  }
</style>