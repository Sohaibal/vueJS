<template>
     <div></div>
</template>


 <script>
  export default {
    name:'ChangeTab',
    mounted() {
      document.addEventListener("visibilitychange", this.handleVisibilityChange);
    },
     methods: {
      handleVisibilityChange() {
        if (!document.hidden) {
          this.showNotification();
        }
      },
      showNotification() {
        // Add your notification logic here
        alert("Welcome back! You switched back to this tab.");
      }
    }
  
    }
   
   </script>