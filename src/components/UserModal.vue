<template>
  <div id="UserModal" @click="setOpenModal">
    <div id="userContainer">
      <img src="../../public/Images/UserIcon.svg" />
      <div id="userName">김민수님</div>
    </div>
    <div class="modalItems">
      <div>마이페이지</div>
    </div>
    <div class="modalItems">
      <div>기본정보 수정</div>
    </div>
    <div class="modalItems">
      <div>1회 체험 신청 내역</div>
    </div>
    <div class="modalItems">
      <div>알림</div>
    </div>
    <div class="modalItems">
      <div>로그아웃</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserModal",
  props:['setOpenModal']
};
</script>

<style scoped lang="scss">
#UserModal {
  width: 132px;
  display: flex;
  flex-direction: column;
  border-radius: 16px;
  > div {
    width: 100%;
    height: 32px;
    padding: 4px 8px;
    display: flex;
    font-size: 12px;
    align-items: center;
    justify-content: start;
  }
}
#userContainer {
  display: flex;
  align-items: center;
  height: 20px;
  margin-right: 24px;
  font-size: 16px !important;
  gap: 16px;
  color: #3d454d;
  font-weight: 400;
}
</style>
