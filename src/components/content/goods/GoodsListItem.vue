<template>
  <div class="goods-item" @click="goToDetail">
    <img v-lazy="showImage" @load="imgLoad" />
    <div class="goods-info">
      <p>{{goodsItem.title}}</p>
      <span class="price">{{goodsItem.price}}</span>
      <span class="collect">
        <img src="~assets/img/common/collect.svg" />
        {{goodsItem.cfav}}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "GoodsListItem",
  props: {
    goodsItem: {
      type: Object,
      default() {
        return {};
      }
    }
  },
  computed: {
    showImage() {
      return this.goodsItem.image || this.goodsItem.show.img;
    }
  },
  methods: {
    imgLoad() {
      this.$bus.$emit("itemImgLoad");
    },
    goToDetail() {
      if (this.$route.fullPath.indexOf("/detail") === -1) {
        var id = this.goodsItem.iid || this.goodsItem.item_id;
        this.$router.push({
          path: "/detail",
          name: "detail",
          params: { iid: id }
        });
      }
    }
  }
};
</script>

<style lang="less" scoped>
.goods-item {
  padding-bottom: 40px;
  position: relative;
  width: 48%;
}
.goods-item img {
  width: 100%;
  border-radius: 5px;
}
.goods-info {
  font-size: 12px;
  position: absolute;
  bottom: 5px;
  left: 0;
  right: 0;
  overflow: hidden;
  text-align: center;
}
.goods-info p {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-bottom: 3px;
}
.goods-info .price {
  color: var(--color-high-text);
  margin-right: 20px;
}
.goods-info .collect {
  position: relative;
}
.goods-info .collect img {
  position: absolute;
  left: -15px;
  top: -1px;
  width: 14px;
  height: 14px;
}
</style>