<template>
   <div class="calender-wrapper">
      <table class="table table-bordered">
         <thead>
            <tr>
               <td v-for="(day, i) in days" :key="i" class="text-center" style="height: 80px;">
                  <p class="text-muted mb-0">{{ $moment(day).format('ddd') }}</p>
                  <p class="mb-0 font-weight-bold">{{ $moment(day).format('DD MMM') }}</p>
               </td>
            </tr>
         </thead>
         <tbody>
            <tr v-for="row in 5" :key="row">
               <td v-for="(col, i) in days.length" :key="i" :id="`${days[i]}-${row}`" style="height: 80px;"></td>
            </tr>
         </tbody>
      </table>

      <!-- Shedules -->
      <div v-for="(shedule, i) in shedules" :key="i" class="shedule-item" :class="`bg-${shedule.position.color}`" :data-x="getPosition(shedule)" :style="{
         'top': shedule.position.top,
         'left': shedule.position.left,
         'width': shedule.position.width,
      }">
         <p class="mb-0">ID #${{shedule.id}}</p>
         <div class="mx-3">
            <p class="mb-0">Start: {{ $moment(shedule.from).format('h:mm a MMM Do YYYY') }}</p>
            <p class="mb-0">End: {{ $moment(shedule.to).format('h:mm a MMM Do YYYY') }}</p>
         </div>
         <div>
            <p class="mb-0">Price</p>
            <p class="mb-0 font-weight-bold">${{ shedule.price }}</p>
         </div>
      </div>

   </div>
</template>

<script>
export default {
   data() {
      return {
         shedules: [
            {
               id: '4500',
               price: 320,
               from: '2022-01-31T18:00:00.000Z',
               to: '2022-02-02T18:00:00.000Z',
               position: {
                  top: '0px',
                  left: '0px',
                  width: '286px',
                  color: 'primary',
                  row: '1'
               }
            },
            {
               id: '4500',
               price: 320,
               from: '2022-02-04T18:00:00.000Z',
               to: '2022-02-05T18:00:00.000Z',
               position: {
                  top: '0px',
                  left: '0px',
                  width: '200px',
                  color: 'info',
                  row: '2'
               }
            },
            {
               id: '4500',
               price: 320,
               from: '2022-02-01T18:00:00.000Z',
               to: '2022-02-02T18:00:00.000Z',
               position: {
                  top: '0px',
                  left: '0px',
                  width: '200px',
                  color: 'success',
                  row: '2'
               }
            },
            {
               id: '4500',
               price: 320,
               from: '2022-02-06T18:00:00.000Z',
               to: '2022-02-07T18:00:00.000Z',
               position: {
                  top: '0px',
                  left: '0px',
                  width: '200px',
                  color: 'danger',
                  row: '1'
               }
            }
         ],
         days: [
            '2022-01-31T18:00:00.000Z',
            '2022-02-01T18:00:00.000Z',
            '2022-02-02T18:00:00.000Z',
            '2022-02-03T18:00:00.000Z',
            '2022-02-04T18:00:00.000Z',
            '2022-02-05T18:00:00.000Z',
            '2022-02-06T18:00:00.000Z',
         ]
      }
   },
   methods: {
      getPosition(shedule) {
         this.$nextTick(() => {
            const fromEl = document.getElementById(`${shedule.from}-${shedule.position.row}`)
            const toEl = document.getElementById(`${shedule.to}-${shedule.position.row}`)

            if (fromEl) {
               const fromPos = this.getOffset(fromEl)
               shedule.position.top = fromPos.top
               shedule.position.left = fromPos.left

               if (toEl) {
                  // const toPos = this.getOffset(toEl)

                  const distance = this.getDistanceBetweenElements(fromEl, toEl)
                  shedule.width = `${distance}px`
               }
            }


         })

      },
      getOffset(el) {
         var rect = el.getBoundingClientRect(),
            scrollLeft = window.pageXOffset || document.documentElement.scrollLeft,
            scrollTop = window.pageYOffset || document.documentElement.scrollTop
         return { top: `${(rect.top + scrollTop).toFixed(0)}px`, left: `${(rect.left + scrollLeft).toFixed(0)}px` }
      },
      getPositionAtCenter(element) {
         const { top, left, width, height } = element.getBoundingClientRect()
         return {
            x: left + width / 2,
            y: top + height / 2
         }
      },
      getDistanceBetweenElements(a, b) {
         const aPosition = this.getPositionAtCenter(a)
         const bPosition = this.getPositionAtCenter(b)

         return Math.hypot(aPosition.x - bPosition.x, aPosition.y - bPosition.y)
      }

   },
}
</script>

<style scoped>
.shedule-item {
   display: flex;
   align-items: center;
   /* background-color: $info; */
   margin: 0.25rem;
   padding: 0.5rem;
   border-radius: 8px;
   color: white;
   position: fixed;
   overflow-x: auto;
   white-space: nowrap;
}

.shedule-item::-webkit-scrollbar {
   display: none;
}
</style>
