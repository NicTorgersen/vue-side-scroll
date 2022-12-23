<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue';

defineProps({
    items: {
        type: Array,
        default() {
            return [];
        },
    }
})

let sideScrollerMax = 0;
const sideScroller = ref(null);
const showIndicator = ref(true);

const onScrollHandler = e => {
    showIndicator.value = e.target.scrollLeft < sideScrollerMax;
}

onMounted(() => {
    sideScrollerMax = sideScroller.value.scrollLeftMax;
    sideScroller.value.addEventListener('scroll', onScrollHandler);
})

onBeforeUnmount(() => {
    sideScroller.value.removeEventListener('scroll', onScrollHandler);
})
</script>

<template>
    <div class="flex">
        <div class="mr-1 relative">
            <span class="absolute npcMovementRight" v-show="!showIndicator">←</span>
        </div>
        <ul ref="sideScroller" class="side-scroller flex">
            <li v-for="item in items">
                <a class="mr-2 underline px-1 block whitespace-nowrap" :href="item.url" v-html="item.innerHtml"></a>
            </li>
        </ul>
        <div class="ml-1 relative">
            <span class="absolute npcMovementLeft" v-show="showIndicator">→</span>
        </div>
    </div>
</template>

<style lang="scss" scoped>
.side-scroller {
    overflow-x: scroll;

    /**
     * hide scrollbar browser styles
     **/
    scrollbar-width: none;
    -ms-overflow-style: none;
    overflow: -moz-scrollbars-none;

    &::-webkit-scrollbar {
        display: none;
    }
}

@keyframes npcMovementLeft {
    0% {
        left: 0;
    }
    30% {
        left: 7.5px;
    }
    100% {
        left: 0;
    }
}

@keyframes npcMovementRight {
    0% {
        right: 0;
    }
    30% {
        right: 7.5px;
    }
    100% {
        right: 0;
    }
}

.npcMovementRight {
    animation: 2s infinite npcMovementRight;
}

.npcMovementLeft {
    animation: 2s infinite npcMovementLeft;
}
</style>
