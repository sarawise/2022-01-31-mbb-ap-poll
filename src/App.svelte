<script>
  import Table from './components/Table.svelte';
  import data from './data/data.json';

  import pym from 'pym.js';

  // Important iframe handling
  new pym.Child({
    polling: 500,
  });

  const cols = [
    {
      label: 'Rank',
      visible: false,
    },
    {
      label: 'Logo',
      visible: false,
      ariaHidden: true,
    },
    {
      label: 'Team',
      visible: false,
      class: 'team',
    },
    {
      label: 'W-L',
      visible: true,
      ariaLabel: 'Win-Loss Record',
    },
    {
      label: 'Points',
      visible: true,
    },
    {
      label: 'Chg.',
      visible: true,
      ariaLabel: 'Change in rank since last week',
    },
  ];
</script>

<div class="chart-container">
  <h1 class="headline">AP Men's Basketball Poll, Week 13</h1>
  <!-- <p class="headline-units">
    <span class="swatch" />Currently in playoffs, as of August 10, 2021
  </p> -->
  <div class="table-container">
    <Table {data} {cols} isSplitTable={true} />
  </div>
</div>

<style>
  @media (min-width: 600px) {
    .table-container {
      display: flex;
      align-items: flex-start;
      gap: 30px;
    }
  }
</style>
