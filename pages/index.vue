<template>
  <div class="container mt-3">
    <h1>
      کادوتو پین کن
    </h1>
    <p>
      برای دیدن پیشنهادات کادویی مناسب همه افراد لطفاثبت نام کنید.
    </p>
    <Form />
  </div>
</template>
<script>
import Form from "@/components/Form"

export default {
  components: {
    Form
  },
}
</script>

<style scoped>
  .mt-3 {
    margin-top: 3rem
  }
</style>
