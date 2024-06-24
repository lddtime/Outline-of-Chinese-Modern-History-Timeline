<template>
  <view class="zero-timeline">
    <view v-for="(item, index) in dataList" :key="index" class="item"
      :style="{ '--color': item.color || '#0396FF', '--bgcolor': item.color ? item.color + '1a' : '#0396FF1a', '--gap': gap, '--left': leftWidth }">
      <view class="left" v-if="showLeft">
        <view class="title">{{ item.time }}</view>
        <view class="sub">{{ item.remarks.join('\n') }}</view>
      </view>
      <view class="line">
        <view class="dot"></view>
      </view>
      <view class="right">
        <view class="card">
          <view class="header">
            <view class="title">{{ item.title }}</view>
            <uni-tag v-if="item.tags.includes('单选')" class="tag" text="单选" size="small" type="success" circle />
            <uni-tag v-if="item.tags.includes('简答')" class="tag" text="简答" size="small" type="warning" circle />
            <uni-tag v-if="item.tags.includes('论述')" class="tag" text="论述" size="small" type="error" circle />
          </view>
          <view class="content">
            <uni-rate v-if="item.stars" :value="item.stars" size="18" color="LightGray" />
            <view class="sub">{{ item.content.join('\n') }}</view>
            <view class="tips">{{ item.sub.join('\n') }}</view>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  name: "zero-timeline",
  props: {
    dataList: {
      type: Array,
      default: () => []
    },
    showLeft: {
      type: Boolean,
      default: true
    },
    leftWidth: {
      type: String,
      default: '300rpx'
    },
    gap: {
      type: String,
      default: '20rpx'
    }
  },
  data() {
    return {

    }
  }
};
</script>

<style lang="scss" scoped>
.zero-timeline {
  position: relative;
  padding: 10rpx;
  display: flex;
  flex-direction: column;

  .item {
    display: flex;
  }

  .left {
    width: var(--left);
    overflow: hidden;
    margin-bottom: var(--gap);
    text-align: right;
    white-space: pre-wrap;
    word-wrap: break-word;
    word-break: break-all;
    flex-shrink: 0;

    .title {
      color: var(--color);
      font-size: 32rpx;
      font-weight: 500;
    }

    .sub {
      color: #999999;
      font-size: 24rpx;
    }
  }

  .line {
    margin: 2px 10px 0px 10px;
    width: 2px;
    background: #eeeeee;
    position: relative;
    flex-shrink: 0;
    flex-grow: 0;

    .dot {
      position: absolute;
      top: 0px;
      left: 50%;
      transform: translateX(-50%);
      display: flex;
      justify-content: center;
      align-items: center;
      width: 8px;
      height: 8px;
      background: var(--color);
      box-shadow: 0 0 3px 1px var(--color);
      border-radius: 50%;
    }
  }

  .right {
    flex: 1;
    margin-bottom: var(--gap);

    .card {
      padding: 20rpx 30rpx;
      min-height: 50rpx;
      background: var(--bgcolor);
      border-radius: 10rpx;
      white-space: pre-wrap;
      word-wrap: break-word;
      word-break: break-all;

      .header {
        display: flex;
        align-items: center;

        .title {
          font-weight: 600;
          color: var(--color);
          font-size: 38rpx;
        }

        .tag {
          margin-left: 20rpx;
        }
      }

      .sub {
        color: #666666;
        font-size: 30rpx;
        padding: 5rpx 0;
      }

      .tips {
        color: #999999;
        font-size: 28rpx;
      }
    }

  }

  .item:last-child {
    .line {
      background: transparent;
    }
  }
}
</style>
