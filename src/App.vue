<template>
    <div id="app">
        <HelloWorld :parentStuff.sync="stuff" />
        <pre>{{ Stuff }} </pre>
    </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";

const parentObj = { name: "I'm from the parent", shoeSize: 3 };

export default {
    name: "App",
    components: {
        HelloWorld,
    },
    data() {
        return {
            stuff: { ...parentObj },
        };
    },
};
</script>
