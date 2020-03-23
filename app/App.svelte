<script>
  import { onMount } from "svelte";
  const api_token =
    "CmugEvLuBxQDjGeVWEbj1mylj0OoeHn7FwGMl5KDvGkU0RgWs9RYYRSjjdmV";
  //Vi må ha url med https, så putt en 's' etter http
  const url = `https://api.worldtradingdata.com/api/v1/stock?symbol=SNAP,TWTR,VOD.L&api_token=${api_token}`;

  let data = [];

  onMount(() => {
    fetch(url)
      .then(response => response.json())
      .then(json => {
        data = json.data;
      })
      .catch(error => console.log(error));
  });
</script>

<style>
  .container {
    background-color: #eee;
  }
  .text-color {
    color: #444;
  }
  .card {
    background-color: white;
    box-shadow: 2 2 #444;
    padding: 8;
    margin: 8 16;
    border-radius: 4;
  }
</style>

<page>
  <actionBar title="Stocks'n'shit" />
  <gridLayout>
    <scrollView>
      <stackLayout class="container">
        {#each data as stock}
          <stackLayout class="card">
            <label class="body text-color" text={stock.name} />
            <label class="text-color" text="{stock.currency} {stock.price}" />
          </stackLayout>
        {:else}
          <activityIndicator busy={true} />
        {/each}
      </stackLayout>
    </scrollView>
  </gridLayout>
</page>
