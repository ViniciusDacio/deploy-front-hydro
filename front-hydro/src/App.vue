<script setup>
var show = false;
console.log($cookies.get("token"));
if ($cookies.get("token")) {
  show = true;
} else {
  show = false;
}
</script>

<template>
  <RouterView />
</template>
