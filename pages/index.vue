<template>
  <h1 class="text-center mt-4">建立訂單</h1>
  <div class="w-50 mx-auto mt-4">
    <form action="#" @submit.prevent="createOrder">
      <div class="mb-3">
        <label for="email" class="form-label">買家信箱</label>
        <input type="email" class="form-control" id="email" v-model="email" />
      </div>
      <div class="mb-3">
        <label for="title" class="form-label">訂單標題</label>
        <input type="text" class="form-control" id="title" v-model="title" />
      </div>
      <div class="mb-3">
        <label for="amount" class="form-label">訂單總額</label>
        <input
          type="number"
          class="form-control"
          id="amount"
          v-model="amount"
        />
      </div>
      <div class="text-end">
        <button
          type="submit"
          class="btn btn-primary"
          @click.prevent="createOrder"
        >
          建立
        </button>
      </div>
    </form>
  </div>
</template>

<script setup lang="ts">
const email = ref('');
const title = ref('');
const amount = ref('');

const router = useRouter();

const createOrder = async () => {
  const method = 'POST';
  const body = { email: email.value, title: title.value, amount: amount.value };

  const { order } = await $fetch('/api/orders', { method, body });

  if (order?.id) router.push(`/${order.id}`);
};
</script>
