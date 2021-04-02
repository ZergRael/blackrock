<template>
  <td>
    {{
      buffs
        ? buffs.buffs.map((e) => e.b + (e.c > 1 ? `(${e.c})` : "")).join(",")
        : ""
    }}
  </td>
</template>

<script>
export default {
  name: "Cell",
  props: ["fight", "buffs"],
};
</script>
