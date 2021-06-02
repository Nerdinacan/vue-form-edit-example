<template>
    <div>
        <b>Editing Form</b>
        <input v-model="name" />
        <input v-model="shoeSize" />
        <pre>{{ stuff }}</pre>
    </div>
</template>

<script>
export default {
    props: {
        stuff: { type: Object, required: true },
    },
    computed: {
        // You can either make a computed with a setter
        name: {
            get() {
                return this.stuff.name || "";
            },
            set(newName) {
                this.emitUpdate({ name: newName });
            },
        },
        shoeSize: {
            get() {
                return this.stuff.shoeSize || 1;
            },
            set(newShoeSize) {
                this.emitUpdate({ shoeSize: newShoeSize });
            },
        },
    },
    methods: {
        emitUpdate(updates = {}) {
            // emit a whole new object
            const newStuff = { ...this.stuff, ...updates };
            this.$emit("update:stuff", newStuff);
        },
    },
};
</script>