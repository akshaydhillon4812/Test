<template>
  <div class="hello">
    <div class="row">
    <!-- Colum 1 -->
    <div class="col-sm-6">
      <div class="row" style="margin-top:7%;">
          <div class="col-sm-2"></div>
          <div class="col-sm-8">
          <h4>Enter Email Address</h4>
          <input type="text" v-model="email"/>
          <br/>
          <br/>
          <b-button @click="addEmailAdd()" variant="primary" class="col-sm-2" > Add</b-button>
          </div>
          <div class="col-sm-2"></div>

      </div>
    </div>
    
    <!-- Column 2-->
    <div class="col-sm-6">
      <div class="row" style="margin-top:7%;">

        <div class="col-sm-2"> </div>
        <div class="col-sm-8">
            <input type="text" class="col-sm-12" v-model="keyword" placeholder="Enter a Keyword to Start Searching" >
            <br/>
            <div >
                <input type="checkbox" v-model="showOnlyEnabled"> Show only enabled  
            </div>

              <div class="row" style="margin-top:20px; max-height:50vh;min-height:50vh;overflow-y:scroll;">
                  <table class="table">
                  <tr>
                      <th>isEnabled</th>
              
                      <th>Email</th>
          
                      <th>Delete</th>
                  </tr>

                  <tr v-for="(emailObj,index) in listOfEmailAdd"  v-if="emailObj.email.includes(keyword) && (!showOnlyEnabled || emailObj.isEnabled )">
                    <td><input type="checkbox" v-model="emailObj.isEnabled"></td> <td> {{emailObj.email }}</td><td><img src="../assets/delete-icon.png" @click="removeRow(index,emailObj.email)"> </td>
           
                  </tr>

                </table>

              </div>
        </div>
        <div class="col-sm-2"> </div>
    </div>
  </div>
</div>



  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data: function()
  {
      return {
        email:'',
        listOfEmailAdd:[],
        emailAddHashTable:{},
        keyword:'',
        showOnlyEnabled:false,
       }
  },
  methods:{

  addEmailAdd()
  {
      if(this.emailAddHashTable[this.email]!=null)
        {
          alert("Email address already exist");
          return ;
        }if(!this.validateEmail(this.email))
        {
          alert("Please enter a valid email address");
          return ;
        }
      var obj={};
      obj.email=this.email;
      obj.isEnabled=true;
      this.emailAddHashTable[this.email]="exist";
      this.listOfEmailAdd.push(obj);

  },
  removeRow(index,email)
  {
    this.listOfEmailAdd.splice(index,1);
    delete this.emailAddHashTable[email];
  },
  validateEmail(email) {
    var re = /^(([^<>()\[\]\\.,;:\s@"]+(\.[^<>()\[\]\\.,;:\s@"]+)*)|(".+"))@((\[[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\])|(([a-zA-Z\-0-9]+\.)+[a-zA-Z]{2,}))$/;
    return re.test(String(email).toLowerCase());
}
  }
} 
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
tr
{
  border-style:none;
}
</style>
