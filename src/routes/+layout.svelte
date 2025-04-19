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
  class="flex items-center space-x-5 border-b-1 border-b-stone-300 h-15 px-2 text-xl text-white dark:border-b-stone-800 dark:bg-stone-950"
>
  <img src="logo.svg" alt="logo" class="size-10" />
  <a
    href="/home"
    class={["px-1 underline-offset-2", route == "/home" && "underline"]}
  >
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
  class="fixed flex justify-center inset-0 top-15 overflow-y-scroll bg-white dark:bg-linear-0 dark:from-black dark:to-stone-900"
>
  <article
    class="md:m-10 m-0 prose md:min-w-250 md:rounded-md md:border-1 md:border-stone-300 md:bg-white p-10 md:dark:border-stone-800 dark:bg-stone-950 dark:prose-invert"
  >
    {@render children()}
  </article>
</div>
