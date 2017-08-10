# vue-laravel-pagination
Vue component that provides offset navigation with Laravel 5

* Import the module with:
  
Vue.component('pagination', require('./Pagination.vue'));
  
* You need to pass the current page and the last page:

\<pagination :current="current_page" :last="last_page" v-on:paginate="onPaginatorClicked($event)"\>\</pagination\>
  
* Alternativelly, you can set the offset and the align (via bootstrap align classes). The component emits a 'paginate' event to be catched
