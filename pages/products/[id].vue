<template>
  <div>
    <Head>
      <Title>Nuxt Dojo | {{product.title }}</Title>
      <Meta name="description" :content="product.description" />
    </Head>
    <ProductDetails :product="product" />
  </div>
</template>

<script setup>
definePageMeta({
  layout: "products",
});
const { id } = useRoute().params;
const url = `https://fakestoreapi.com/products/${id}`;

// fetch product
const { data: product } = await useFetch(url, { key: id });

if (!product.value) {
  throw createError({
    statusCode: 404,
    message: "Product not found",
    fatal: true,
  });
}
</script>

<style lang="scss" scoped>
</style>