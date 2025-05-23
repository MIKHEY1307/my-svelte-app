<script lang="ts">
  import { page } from '$app/stores';
  import { onMount } from 'svelte';
  import { get } from 'svelte/store';

  let userId: string | null = null;
  let userData: any = null;

  onMount(async () => {
    const query = new URLSearchParams(get(page).url.search);
    userId = query.get('user') ?? '1';
    const res = await fetch(`https://jsonplaceholder.typicode.com/users/${userId}`);
    userData = await res.json();
  });
</script>

{#if userData}
  <h1>Профиль пользователя: {userData.name}</h1>
  <p>Email: {userData.email}</p>
{:else}
  <p>Загрузка...</p>
{/if}
