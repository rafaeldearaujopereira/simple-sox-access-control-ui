<script>

export default {
  name: "navItem",
  props: {
    code: String,
    featureTree: Object
  },
  emits: ["navigateTo"],
  setup(props, { emit }) {
    const open = () => {
      console.log("open : " + props.code);
      emit("navigateTo", props.code);
    }
    return { open };
  },
};
</script>

<template>
  <li class="nav-item"><a class="nav-link active" @click.prevent="open" aria-current="page" href="#"><slot></slot></a></li>
</template>