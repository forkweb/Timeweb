<template>
  <div class="content pagination">
    
      <ul class="pagination__list">
        <button @click="changePage(currentPage-1)" v-if="hasPrev()">Previous</button>
        <li v-for="p in totalPages" :key="p">
          <button class="pagination-button" :class="{active: currentPage === p}" @click="changePage(p)">{{p}}</button>
        </li>
        <button @click="changePage(currentPage+1)" v-if="hasNext()">Next</button>
      </ul>

  </div>
</template>

<script>
  export default {
    name: "Pagination",
    props: ['total', 'item'],
    data(){
      return {
        currentPage: 1,
      }
    },
    computed: {
      totalPages() {

        return Math.ceil(this.total / this.item);
      }
    },
    methods: {
      hasPrev(){
        return this.currentPage > 1;
      },
      hasNext(){
        return this.currentPage < this.totalPages;
      },
      changePage(pageNumber) {
        this.currentPage = pageNumber;
        this.$emit('page-changed', pageNumber);
        // this.currentPage = this.totalPages;
      }
    }
  }
</script>


<style scoped>

  .pagination-button {
    background-color: white;
    color: teal;
    border: 1px solid #3b5998;
  }

  .active {
    background-color: rgb(213 38 239 / 31%);
  }

</style>
