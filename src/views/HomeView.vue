<script setup>
import Timer from "../components/Timer.vue";
</script>

<template>
  <main>
    <table>
      <tr>
        <Timer />    
      </tr>
      <tr>
        <td>
          <Timer :default-sec-start='30'/>
        </td>
        <td>
          <Timer :default-sec-start='60'/>
        </td>
      </tr>
      <tr>
        <td>
          <Timer :default-min-start='5'/>
        </td>
        <td>
          <Timer :default-min-start='10'/>
        </td>
        <td>
          <Timer :default-min-start='15'/>
        </td>
        <td>
          <Timer :default-min-start='30'/>
        </td>
      </tr>
    </table>
    
    
  </main>
</template>
