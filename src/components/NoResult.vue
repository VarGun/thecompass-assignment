<template>
  <div class="NoResult">
    <div>검색결과가 없습니다.</div>
  </div>
</template>

<script>
export default {
  name: "NoResult",
  props: {
    msg: String,
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.NoResult {
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 16px;
  color: #6c7680;
  width: 472px;
  height: 52px;
}
</style>
