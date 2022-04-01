<template>
  <div>
    <div class="container">
      <div class="row justify-content-center">
        <div class="col-6">
            <h1 class="text-primary text-center">Invoice Maker <a href="http://localhost:8080/" target="_blank" class="btn btn-primary"><i class="fas fa-file-invoice"></i></a></h1>
            <form action="" class="m-5" @submit.prevent="submitItems">
                <div class="row g-1">
                   <div class="col-6">
                     <div class="form-group" >
                        <select  name="" id="" class="form-select" v-model="selectedItem" required>
                          <option value="" disabled>Choose Your Products</option>
                          <option v-for="item in items" :key="item.id" :value="item.id">
                            {{item.name}}
                            </option>
                        </select>
                     </div>
                   </div>
                   <div class="col">
                     <div class="form-group">
                        <input type="text" placeholder="Quantity" v-model.number="selectedQuantity" required class="form-control">
                     </div>
                   </div>
                   <div class="col">
                     <button class="btn btn-primary w-100">
                       <i class="fa-solid fa-plus"></i>
                     </button>
                   </div>
                </div>
            </form>
            <table class="table table-bordered text-center">
                <thead>
                    <tr>
                      <th>id</th>
                      <th>Name</th>
                      <th>Price Per Unit</th>
                      <th>Quantity</th>
                      <th>Total Cost</th>
                    </tr>
                </thead>
                <tbody>
                  <tr v-for="(item,index) in newItems" :key="index">
                    <td><i class="fas fa-trash text-danger" @click="removeItem(index)"></i></td>
                    <td>{{item.product.name}}</td>
                    <td>{{item.product.price}}</td>
                    <td>{{item.quantity}}</td>
                    <td>{{item.totalPrice}}</td>
                  </tr>
                </tbody>
                <tfoot v-if="newItems.length>0">
                  <tr>
                    <td colspan="4">Total Cost</td>
                    <td>{{total}}</td>
                  </tr>
                </tfoot>
            </table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
 
      data() {
        return {
          selectedItem:"",
          selectedQuantity:"",
          items:[
            {id:1,name:"phone",price:100},
            {id:2,name:"PS5",price:140},
            {id:3,name:"Food Pack",price:10},
            {id:4,name:"Water And Energy Drinks",price:5}
          ],
          newItems:[],
        }
      },
      methods:{
        submitItems(){
          if(this.selectedItem && this.selectedQuantity && Number(this.selectedQuantity)){
            let selectProduct=this.items.find(el=>el.id===this.selectedItem);
            let totalCost=selectProduct.price * this.selectedQuantity;
            let newItem={quantity:this.selectedQuantity,totalPrice:totalCost,product:selectProduct};
            this.newItems.push(newItem);
            console.log(this.newItems);

            this.selectedItem='';
            this.selectedQuantity='';
          }else{
            alert("No Data");
          }
        },
        removeItem(index){
          this.newItems=this.newItems.filter((el,i)=> i !== index);
        }
      },
      computed:{
        total(){
           return this.newItems.reduce((p,s)=> p+s.totalPrice, 0);
        }
      }
}
</script>

<style lang="scss">



</style>