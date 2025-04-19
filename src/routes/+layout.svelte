<script lang="ts">
  import { page } from "$app/state";
  import { onNavigate } from "$app/navigation";
  import "../app.css";

  onNavigate((navigation) => {
    if (!document.startViewTransition) return;

    return new Promise((resolve) => {
      document.startViewTransition(async () => {
        resolve();
        await navigation.complete;
      });
    });
  });

  const { children } = $props();

  const route = $derived(page.route.id);
</script>

<nav
  class="flex h-15 items-center space-x-5 border-b-1 border-b-stone-300 px-2 text-xl text-white dark:border-b-stone-800 dark:bg-stone-950"
>
  <img src="logo.svg" alt="logo" class="size-10" />
  <a href="/" class={["px-1 underline-offset-2", route == "/" && "underline"]}>
    Home
  </a>
  <a
    href="/projects"
    class={["px-1 underline-offset-2", route == "/projects" && "underline"]}
  >
    Projects
  </a>
  <a
    href="/homelab"
    class={["px-1 underline-offset-2", route == "/homelab" && "underline"]}
  >
    Homelab
  </a>
</nav>

<div
  class="fixed inset-0 top-15 flex justify-center overflow-y-scroll bg-white dark:bg-linear-0 dark:from-black dark:to-stone-900"
>
  <article
    class="m-0 prose p-10 md:m-10 md:min-w-250 md:rounded-md md:border-1 md:border-stone-300 md:bg-white dark:bg-stone-950 dark:prose-invert md:dark:border-stone-800"
  >
    {@render children()}
  </article>
</div>
