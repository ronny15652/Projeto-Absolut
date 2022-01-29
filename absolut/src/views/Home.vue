<template>
<div>
    <Banner />
    <FormPedido />
</div>
</template>

<script>
import Banner from '../components/home/Banner.vue'
import FormPedido from '../components/home/FormPedido.vue'
export default {
    components: {
        Banner,
        FormPedido
    }
}
</script>
