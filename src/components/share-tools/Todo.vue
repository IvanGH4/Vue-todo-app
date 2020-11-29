<template>
  <ul class="p-0">
    <li class="my-3 p-2">
      <p :class="[myClass, completedTask ? 'complete-todo' : 'null']">
        {{ text }}
      </p>
      <div>
        <span @click="myFunc(id)" class="material-icons mr-3">{{ icono }}</span
        ><i @click="myOther(id)" class="fas fa-trash"></i>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  name: "Todo",
  props: {
    id: {
      type: Number,
      default: 0,
    },
    text: {
      type: String,
      default: "",
    },
    completedTask: {
      type: Boolean,
      default: false,
    },
    icono: {
      type: String,
      default: "check",
    },
    myClass: {
      type: String,
      default: "",
    },
    myFunc: {
      default: "",
    },
    myOther: {
      default: "",
    },
  },
};
</script>