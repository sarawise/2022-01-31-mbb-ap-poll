<script>
  import TableHead from "./TableHead.svelte";
  import TableItemRow from "./TableItemRow.svelte";
  export let data;
  export let cols;
  export let isSplitTable;

  let tables = [];
  if (isSplitTable) {
    const half = Math.ceil(data.length / 2);
    tables[0] = data.slice(0, half);
    tables[1] = data.slice(half, data.length);
  }
</script>

<!-- Mobile Table: All Rows -->
<table class="table is-mobile">
  <TableHead {cols} />
  <tbody>
    {#each data as row, index}
      <TableItemRow {row} {index} />
    {/each}
  </tbody>
</table>

<!-- Desktop Table: Split -->
{#if isSplitTable}
  {#each tables as table, i}
    <table class="table is-newsletter">
      <caption class="sr-only"
        >{i === 0 ? "Top" : "Bottom"} half of the rankings</caption
      >
      <TableHead {cols} hideHeader={isSplitTable && i !== 0 ? true : false} />
      <tbody>
        {#each table as row, index}
          <TableItemRow {row} {index} />
        {/each}
      </tbody>
    </table>
  {/each}
{/if}

<style>
  :global(:root) {
    /* Space between table cells */
    --cell-spacing: 6px;
  }

  .table {
    width: 100%;
    border-collapse: collapse;
  }
</style>
