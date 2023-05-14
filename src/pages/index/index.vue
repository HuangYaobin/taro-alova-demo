<template>
  <view class="index">
    <button @click="query">发送请求</button>
  </view>
</template>

<script setup lang="ts">
import { useRequest, createAlova } from 'alova';
import VueHook from 'alova/vue';
import AdapterTaroVue from '@alova/adapter-taro/vue';
import { watchEffect } from 'vue';

const request = createAlova({
  baseURL: 'https://zj.v.api.aa1.cn/api',
  ...AdapterTaroVue(),
  statesHook: VueHook
});

const { loading, data, send } = useRequest(
  (params = { code: '654028207201' }) => request.Get('/xz/', { params }),
  { force: true }
)

const query = () => {
  send({ code: '654028207202' })
}

watchEffect(() => {
  console.log({ loading: loading.value });
  console.log({ data: data.value });
})
</script>
