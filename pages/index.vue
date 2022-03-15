<template>
   <section class="mt-3">
      <div class="container">
         <!-- Header Row -->
         <div class="row">
            <div class="col-6">
               <div class="d-flex justify-content-between align-items-center">
                  <b-form-datepicker v-model="form.date" class="mr-2"></b-form-datepicker>
                  <b-form-select v-model="form.selected" :options="options"></b-form-select>
               </div>
            </div>
            <div class="col-6">
               <div class="d-flex justify-content-end">
                  <b-form-input v-model="form.search" placeholder="Search" class="w-50"></b-form-input>
               </div>
            </div>
         </div>

         <!-- Table of content -->
         <div class="row mt-4">
            <!-- Left sidebar -->
            <div class="col-4">
               <div class="border">
                  <p class="text-center py-2 mb-0 border-bottom">Vehicles</p>

                  <!-- Vehicles List -->
                  <b-card no-body v-for="item in 4" :key="item" @click="activeVehicle = item" :class="{active: item == activeVehicle}" class="vehicle-item rounded-0 border-0 p-2 pointer">
                     <b-row no-gutters class="align-items-center">
                        <b-col md="4">
                           <b-card-img src="https://picsum.photos/400/400/?image=20" alt="Image" class="" style="height: 75px;"></b-card-img>
                        </b-col>
                        <b-col md="8">
                           <b-card-body class="pl-3 pr-2 py-2">
                              <b-card-text>
                                 <h6 class="mb-1">Category Name</h6>
                                 <p class="mb-1">subtitle here</p>

                                 <div>
                                    <span class="bg-success dot"></span>
                                    <span>14</span>
                                 </div>
                              </b-card-text>
                           </b-card-body>
                        </b-col>
                     </b-row>
                  </b-card>
               </div>
            </div>

            <!-- Right content -->
            <div class="col-8">
               <!-- Days -->
               <div class="days-grid">
                  <div v-for="(day, i) in days" :key="i" class="text-center border py-2">
                     <p class="text-muted mb-0">{{ day.name }}</p>
                     <p class="mb-0 font-weight-bold">{{ day.date }}</p>
                  </div>
               </div>

               <div class="empty-box-grid">
                  <div v-for="item in (7*6)" :key="item" class="border" style="height: 90px;"></div>
               </div>

            </div>
         </div>
      </div>
   </section>
</template>

<script>
export default {
   name: 'IndexPage',
   data() {
      return {
         activeVehicle: 1,
         form: {
            date: '2022-03-15',
            selected: 'x',
            search: ''
         },
         options: [
            { value: 'x', text: 'Weekly View' },
            { value: 'a', text: 'This is First option' },
            { value: 'b', text: 'Selected Option' },
            { value: 'c', text: 'This is an option with object value' }
         ],
         days: [
            { name: 'TUE', date: '01 Feb' },
            { name: 'WED', date: '02 Feb' },
            { name: 'THU', date: '03 Feb' },
            { name: 'FRI', date: '04 Feb' },
            { name: 'SAT', date: '05 Feb' },
            { name: 'SUN', date: '06 Feb' },
            { name: 'MON', date: '07 Feb' },
         ]
      }
   }
}
</script>

<style scoped>
.dot {
   width: 12px;
   height: 12px;
   border-radius: 50%;
   display: inline-block;
}

.vehicle-item.active {
   background: rgb(241, 239, 239);
}

.days-grid {
   display: grid;
   grid-template-columns: repeat(7, 1fr);
}

.empty-box-grid {
   display: grid;
   grid-template-columns: repeat(7, 1fr);
}
.pointer {
   cursor: pointer;
}
</style>
