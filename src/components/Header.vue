<template>
  <div>
   <b-nav>
    <b-nav-item><b>Fancy Quiz App</b></b-nav-item>
    <b-nav-item disabled>Counter: {{numCorrect}}/{{numTotal}}</b-nav-item>
   </b-nav>
  </div>
</template>

<script nonce>

    export default {
        props: [
            'numCorrect',
            'numTotal'
        ]
    }
</script>