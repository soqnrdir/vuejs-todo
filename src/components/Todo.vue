<template>
    <div style="text-align:left;" class="mb-2 d-flex">
        <div>
            <input type="checkbox" :checked="todo.checked" 
            @change="toggleCheckbox">
        </div>
        <!-- class, style 바인딩으로 해당항목이 체크가 되어있으면 이벤트 아니면 그대로 두는 코드를 작성 -->
        <span style="margin-left:3px" class="flex-grow-1"
            :class="todo.checked ? 'text-muted' : ''"
            :style="todo.checked ? 'text-decoration:line-through': ''"
        >{{ todo.text }}</span>
        <button class="btn btn-danger btn-sm"
            @click="clickDelete"
        >Delete</button>
    </div>
</template>

<script>
export default {
    props: {
        todo: {
            type: Object,
            required: true
        }
    },
    methods: {
        toggleCheckbox(e) {
            this.$emit('toggle-checkbox', {
                id: this.todo.id,
                checked: e.target.checked
            })
        },
        clickDelete() {
            this.$emit('click-delete', this.todo.id);
        }
    }
}
</script>