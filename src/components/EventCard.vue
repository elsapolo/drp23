<template>
  <n-card :title="data.name">
    <template #cover>
      <img :src="data.image_url" />
    </template>
    <template #header-extra> {{ data.society }} </template>
    <n-tag
      rounded
      :bordered="false"
      type="success"
      v-if="data.ticket_price === 0"
      >FREE</n-tag
    >
    <n-tag rounded :bordered="false" type="error" v-else>
      £{{ data.ticket_price }}</n-tag
    >
    <n-divider />
    <n-ellipsis expand-trigger="click" line-clamp="2" :tooltip="false">
      {{ data.description }}
    </n-ellipsis>
    <n-divider />

    <em></em>
    {{ data.location }} - {{ prettyPrint(data.date_time) }}:
    <n-space>
      <n-tag v-for="tag in data.tags" :key="tag">{{ tag }}</n-tag>
    </n-space>
    <template #footer>
      <router-link :to="`/event/${data?.event_id || data?.objectID}`">
        view
      </router-link>
    </template>
  </n-card>
</template>

<script lang="ts">
import { NCard, NDivider, NEllipsis, NSpace, NTag } from "naive-ui";
import { defineComponent } from "vue";
interface EventPayload {
  name: string;
  description: string;
  image_url: string;
  society: string;
  location: string;
  date_time: string;
  ticket_price: number;
  latitude: number;
  longitude: number;
  event_id?: string;
  objectID?: string;
  tags: string[];
}

export default defineComponent({
  name: "EventCard",
  components: {
    NCard,
    NTag,
    NSpace,
    NDivider,
    NEllipsis,
  },
  props: {
    data: {
      type: Object as () => EventPayload,
      required: true,
    },
  },
  methods: {
    prettyPrint(date: string) {
      return new Date(date).toLocaleString();
    },
  },
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.n-card {
  max-width: calc(min(100vw, 400px) - 40px);
  margin: 20px;
}
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
