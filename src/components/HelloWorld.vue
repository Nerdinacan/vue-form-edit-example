<template>
    <div>
        <p>
            So this is the parent component. It's holding on to some data
            object. When it changes you'll save it or do whatever you want, but
            the goal is to offload editing to the child form component.
        </p>

        <!-- If you are storing myStuff locally you can handle it this way -->
        <div>
            <h2>Editing local data</h2>
            <EditMyStuff :stuff.sync="myStuff" />
            <pre>{{ myStuff }}</pre>
        </div>

        <!-- if you are passing the changes up the tree to some other component,
        you can handle it using a computed value with a setter -->
        <div>
            <h2>Editing data that came in as a prop</h2>
            <EditMyStuff :stuff.sync="localParentStuff" />
        </div>
    </div>
</template>

<script>
import EditMyStuff from "./EditMyStuff";

export default {
    components: {
        EditMyStuff,
    },
    props: {
        parentStuff: {
            type: Object,
            required: true,
        },
    },
    data() {
        return {
            myStuff: { name: "foo", shoeSize: 1 },
        };
    },
    computed: {
        localParentStuff: {
            get() {
                return this.parentStuff;
            },
            set(newObj) {
                // Here the data that we're editing came from outside as a prop, but you don't
                // modify props, you emit events to change things
                this.$emit("update:parentStuff", newObj);
            },
        },
    },
    watch: {
        myStuff() {
            console.log("my data changed, save it, do whatever");
        },
    },
};
</script>
