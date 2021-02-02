<template>
    <div class="dropdown" ref="dropdownRef">
        <a href="#" class="btn btn-primary my-2 dropdown-toggle" @click.prevent="toggleOpen">{{ title }}</a>
        <ul class="dropdown-menu" :style="{display: 'block'}" v-if="isOpen">
            <!--<li class="dropdown-item">
                <a href="#">新建文章</a>
            </li>
            <li class="dropdown-item">
                <a href="#">编辑资料</a>
            </li>-->
            <slot></slot>
        </ul>
    </div>
</template>

<script lang="ts">
import { defineComponent, ref, watch} from 'vue';
import useClickOutside from "@/hooks/useClickOutside";

export default defineComponent({
    name: 'Dropdown',
    props: {
        title: {
            type: String,
            required: true,
        },
    },

    setup() {
        const isOpen = ref(false);
        const dropdownRef = ref<null | HTMLElement>(null);

        const toggleOpen = () => {
            console.log('toggle')
            isOpen.value = !isOpen.value
        }

        const isClickOutside = useClickOutside(dropdownRef);

        watch(isClickOutside, () => {
            if (isOpen.value && isClickOutside.value) {
                isOpen.value = false
            }
        });

        return {
            isOpen,
            toggleOpen,
            dropdownRef,
        }
    }
});
</script>

<style scoped>

</style>
