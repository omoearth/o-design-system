<script lang="ts">
  import {o, Router} from "@omoearth/o-types";
  import Route from "../1-Atoms/Route.svelte";

  import {onMount} from "svelte";

  onMount(() => {
    //
    // When we already got a key in the localStorage, we can skip the next steps
    // and go straight to the 'transactions' page.
    //
    const privateKey = localStorage.getItem("omo.privateKey");
    const ownerAddress = localStorage.getItem("omo.address");
    const safeAddress = localStorage.getItem("omo.safeAddress");

    if (privateKey && ownerAddress && safeAddress) {
      Router.navigateTo(o.WALLET, "transactions");
    }
  });
</script>

<style>
  .grid {
    display: grid;
    grid-template-rows: 1fr auto;
    position: relative;
  }
</style>

<div class="grid h-full">
  <main class="overflow-y-scroll h-full bg-gray-100 p-8 text-center">
    <h1 class="text-center text-3xl font-title text-primary">Intro Slide</h1>
    <p class="text-sm py-4 text-center text-gray-700">
      Explain your personal money
    </p>
  </main>

  <footer class="flex p-4 border-t border-gray-300">
    <Route dapp={o.WALLET} route="explainsafe">
      <button class="w-full">Next</button>
    </Route>
  </footer>
</div>
