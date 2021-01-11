<template>
    <div class='backdrop' @click.self ='toggleModal'>
      <div class='modal' >
        <h1>Warning</h1>
        <p>Skill Already Exists</p>
      </div>
    </div>
</template>

<script>
export default {
    methods: {
      toggleModal(){
          this.$emit('close')
      }
    }
}
</script>
<style>

  .modal{
      width: 400px;
      background-color: rgb(247, 231, 14);
      padding: 20px;
      margin: 100px auto;
      border-radius: 20px;

  }
  .backdrop{
      width: 100%;
      height: 100%;
      background-color: rgba(0, 0, 0, 0.3);
      position: fixed;
      top:0;
  } 

  .modal h1{
      color: rgb(0, 0, 0);
  }
 
</style>