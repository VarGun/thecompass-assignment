<template>
  <div id="MainHeader">
    <div id="headerSearch">
      <div id="searchTrainer">트레이너 찾기</div>
      <div class="searchOthers">피트니스 센터 찾기</div>
      <div class="searchOthers">PT스튜디오 찾기</div>
    </div>
    <div id="userContainer">
      <img src="../../public/Images/UserIcon.svg" />
      <div id="userName">김민수님</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "MainHeader",
};
</script>

<style scoped lang="scss">
#MainHeader {
  min-width: 100%;
  height: 84px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #ffffff;
  box-shadow: 0px 4px 8px rgba(218, 224, 230, 0.38);

}
#headerSearch {
  display: flex;
  height: 20px;
  gap: 36px;
  flex: none;
  margin-left: 24px;
  > div {
    height: 20px;
    color: #6c7680;
    font-weight: 400;
  }
  #searchTrainer {
    color: #ff8000;
  }
}
#userContainer {
  display: flex;
  align-items: center;
  margin-right: 24px;

  gap: 16px;
  color: #3d454d;
}
</style>
