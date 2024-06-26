<script lang="ts" setup>
import { reactive, ref, watchEffect } from "vue";
import { ElTag, ElSpace } from "element-plus";
import { useJobList } from "./hooks/useJobList";
import { ElTabPane, ElTabs, ElSwitch } from "element-plus";
import { useDeliver } from "./hooks/useDeliver";
const {
  jobList,
  jobMap: { actions: jobMap },
} = useJobList();
const { current } = useDeliver();
const jobListRef = ref<HTMLElement[]>();
const autoScroll = ref(true);
const cards = ref<HTMLDivElement>();
function scroll(e: any) {
  e.preventDefault();
  if (!cards.value) {
    return;
  }
  let left = -e.wheelDelta || e.deltaY / 2;
  cards.value.scrollLeft = cards.value.scrollLeft + left;
  autoScroll.value = false;
}
watchEffect(() => {
  const d = jobListRef.value;
  if (autoScroll.value && d && d.length > current.value) {
    d[current.value].scrollIntoView({
      behavior: "smooth",
      block: "nearest",
      inline: "center",
    });
  }
});

function stateColor(state?: string): string {
  switch (state) {
    case "wait":
      return "#CECECE";
    case "error":
      return "#e74c3c";
    case "warn":
      return "#f39c12";
    case "success":
      return "#2ecc71";
    case "running":
      return "#98F5F9";
  }
  return "#CECECE";
}
</script>

<template>
  <div style="order: -1">
    <div ref="cards" @wheel.stop="scroll" class="card-grid">
      <div
        ref="jobListRef"
        class="card"
        v-for="v in jobList"
        :style="{
          '--state-color': stateColor(jobMap.get(v.encryptJobId)?.state),
          '--state-show': jobMap.has(v.encryptJobId) ? 'block' : 'none',
        }"
      >
        <div class="card-tag">
          {{ v.brandIndustry }},{{ v.jobDegree }},{{ v.brandScaleName }}
        </div>
        <h3 class="card-title">{{ v.jobName }}</h3>
        <h3 class="card-salary">{{ v.salaryDesc }}</h3>
        <div>
          <el-space :size="3" spacer="|" wrap>
            <el-tag
              size="small"
              v-for="tag in v.skills"
              effect="plain"
              type="warning"
            >
              {{ tag }}
            </el-tag>
          </el-space>
          <el-space :size="3" wrap>
            <el-tag
              size="small"
              v-for="tag in v.jobLabels"
              effect="plain"
              type="success"
            >
              {{ tag }}
            </el-tag>
          </el-space>
        </div>
        <div class="card-footer">{{ v.welfareList.join(",") }}</div>
        <div class="author-row">
          <img
            alt=""
            class="avatar"
            height="80"
            :src="v.brandLogo"
            width="80"
          />
          <div>
            <span class="company-name">{{ v.brandName }}</span>
            <h4>
              {{ v.cityName }}/{{ v.areaDistrict }}/{{ v.businessDistrict }}
            </h4>
          </div>
        </div>
        <div class="card-status">
          {{ jobMap.get(v.encryptJobId)?.msg || "无内容" }}
        </div>
      </div>
    </div>
    <el-switch
      v-model="autoScroll"
      inline-prompt
      active-text="自动滚动"
      inactive-text="自动滚动"
    />
  </div>
</template>

<style lang="scss" scoped>
// https://css-tricks.com/
// https://uiverse.io/Subaashbala/polite-newt-9

.card-grid {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  margin: 0 0 1.5rem;
  position: relative;
  overflow-x: scroll;
  scrollbar-color: #c6c6c6 #e9e9e9;
  scrollbar-gutter: always;
  padding: 3rem 0 3rem 2rem;
  margin: 0;
  display: flex;
  color: #000;
  -webkit-overflow-scrolling: touch;
  &::-webkit-scrollbar {
    width: 10px;
    height: 10px;
  }
  &::-webkit-scrollbar-thumb {
    background: #434343;
    border-radius: 10px;
    box-shadow: inset 2px 2px 2px hsla(0, 0%, 100%, 0.25),
      inset -2px -2px 2px rgba(0, 0, 0, 0.25);
  }
  &::-webkit-scrollbar-track {
    background: linear-gradient(
      90deg,
      #434343,
      #434343 1px,
      #262626 0,
      #262626
    );
  }
}
.card {
  --state-color: #f00;
  --state-show: block;
  padding: 1.5rem;
  border-radius: 16px;
  background: linear-gradient(85deg, #f2eeee, #eff0f6);
  color: #000;
  display: flex;
  flex-direction: column;
  transition: 0.2s;
  margin: 0;
  position: relative;
  min-width: 300px;
  min-height: 350px;
  box-shadow: -2rem 0 1rem -2rem #cdb9b9;

  * {
    user-select: none;
  }
  .card-status {
    position: absolute;
    display: var(--state-show);
    border-radius: 30px;
    border-bottom-left-radius: 0;
    border-top-left-radius: 0;
    background-color: var(--state-color);
    color: #fff;
    padding: 7px 17px;
    text-wrap: nowrap;
    font-size: 12px;
    font-weight: bold;
    letter-spacing: 5px;
    left: -6px;
    bottom: -14px;
    transition: all 0.25s ease;
    box-shadow: 1px -7px 12px -2px rgb(167 167 167 / 40%);
  }
  &::after {
    position: absolute;
    content: "";
    display: var(--state-show);
    left: -6px;
    bottom: 18px;
    width: 0;
    height: 0;
    border-left: 6px solid transparent;
    border-right: 0px solid transparent;
    border-bottom: 10px solid oklch(from var(--state-color) calc(l * 0.75) c h);
  }
  .card-tag {
    display: block;
    margin: 0 0 0.25rem;
    color: #6a6868;
    font-size: 0.7rem;
  }
  .card-title {
    font-size: 1.3rem;
    margin: 0 0 8px;
  }
  .card-salary {
    font-size: 1.1rem;
    margin: 0 0 1rem;
    color: #ff442e;
  }
  .card-footer {
    -webkit-margin-before: auto;
    margin-block-start: auto;
    padding: 5px 0;
  }
  .avatar {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    margin-right: 0.5rem;
  }
  .author-row {
    display: grid;
    grid-template-columns: 40px 1fr;
    gap: 0.5rem;
    align-items: center;
    color: #a09f9f;
    line-height: 1.3;
    padding-top: 0.5rem;
    .company-name {
      color: #000;
    }
  }
  &:focus-within,
  &:hover {
    transform: translateY(-1rem) rotate(3deg);
  }

  &:focus-within ~ &,
  &:hover ~ & {
    transform: translateX(130px);
  }

  &:first-child:focus-within,
  &:first-child:hover {
    transform: translate(-0.5rem, -1rem) rotate(3deg);
  }

  &:not(:first-child) {
    margin-left: -130px;
    box-shadow: -3rem 0 3rem -3rem #b4adad;
  }

  @media (max-width: 1200px) {
    & {
      min-width: 250px;
    }

    &:not(:first-child) {
      margin-left: -30px;
    }

    &:hover {
      transform: translateY(-1rem);
    }

    &:hover ~ & {
      transform: translateX(30px);
    }
  }
}

html.dark {
  .card-grid {
    scrollbar-color: #666 #201c29;
    color: #fff;
    &::-webkit-scrollbar-thumb {
      background: #434343;
      box-shadow: inset 2px 2px 2px hsla(0, 0%, 100%, 0.25),
        inset -2px -2px 2px rgba(0, 0, 0, 0.25);
    }
    &::-webkit-scrollbar-track {
      background: linear-gradient(
        90deg,
        #434343,
        #434343 1px,
        #262626 0,
        #262626
      );
    }
  }
  .card {
    background: linear-gradient(85deg, #434343, #262626);
    color: #fff;
    box-shadow: -2rem 0 1rem -2rem #000;

    .card-status {
      color: #fff;

      box-shadow: 1px -7px 12px -2px rgb(167 167 167 / 40%);
    }

    .card-tag {
      color: #b4b4b4;
    }

    .card-salary {
      color: #ff442e;
    }

    .author-row {
      color: #a09f9f;

      .company-name {
        color: #fff;
      }
    }

    &:not(:first-child) {
      box-shadow: -3rem 0 3rem -3rem #000;
    }
  }
}
</style>
