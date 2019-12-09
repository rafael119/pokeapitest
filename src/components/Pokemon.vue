<template>
  <div class="column is-12-mobile is-4-desktop is-4-tablet">
    <div class="card">
      <div class="card-content">
        <h3 class="title is-size-4">{{poke.name}}</h3>
        <h4 class="title has-text-link is-size-6">
          <a v-bind:href="poke.url">{{poke.url}}</a>
        </h4>
        <button class="button is-small is-primary is-rounded" @click="showMore">ver mas</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["poke"],
  mehtods:{
    showMore(id){ 
      this.$emit('showModal',id)
    }
  }
  
};
</script>
