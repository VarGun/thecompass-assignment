<template>
  <div class="LocationWrapper">
    <div class="locationContainer">
      <img src="../../public/Images/LocationColor.svg" />
      <div class="locationText">
        <div class="TextOrange">논현1동</div>
        주변 퍼스널 트레이너
      </div>
    </div>
    <div class="filterContainer">
      <div class="orderingBtn" @click="changeOrderingMode">
        <div>추천순</div>
        <img src="../../public/Images/Dropdown_Down.svg" />
      </div>
      <div class="filterBtn" @click="changeOrderingMode">
        <img src="../../public/Images/Settings.svg" />
        <div class="TextOrange">필터 설정</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "LocationWrapper",
  props: [`orderingMode`],
  methods: {
    changeOrderingMode() {
      this.$emit(`update-mode`, false);
    },
  },
};
</script>

<style scoped lang="scss">
.LocationWrapper {
  width: 480px;
  height: 64px;
  display: flex;
  align-items: center;
  padding: 0px 16px;
  font-weight: 500;
  color: #3d454d;
  gap: 54px;
}
.locationContainer {
  display: flex;
  align-items: center;
  width: 212px;
  height: 24px;
  font-size: 16px;
  gap: 4px;
  > div {
    display: flex;
    flex: none;
  }
}

// font style
.TextOrange {
  color: #ff8000;
}

.filterContainer {
  display: flex;
  align-items: center;
  width: 180px;
  height: 32px;
  gap: 8px;
  > div {
    display: flex;
    align-items: center;
    height: 32px;
    gap: 4px;
    border: 1px solid #dae0e6;
    border-radius: 16px;
    flex: none;
  }
}
.orderingBtn {
  padding: 0px 8px 0px 12px;
}
.filterBtn {
  padding: 0px 12px 0px 8px;
}
</style>
