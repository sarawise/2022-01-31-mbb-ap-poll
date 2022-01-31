<script>
  export let row;

  // Highlight rows with the following key:
  let highlightKey = "Playoffs"; // Column name
  let highlightTrueValue = "Yes"; // What value corresponds with the "highlighted" rows?

  const slugifyTeam = (team) => {
    return team
      .replaceAll("State", "St")
      .replace("&", "")
      .replaceAll(" ", "-")
      .toLowerCase();
  };

  const schoolName = (school) => {
    if (school == "Southern California") {
      return "USC";
    } else if (school == "South Carolina") {
      return "S. Carolina";
    } else {
      let new_name = school.replace("State", "St.");
      return new_name;
    }
  };

  const imgName = (school) => {
    if (school == "Southern California") {
      return "usc.png";
    } else {
      let new_name = school.replace("State", "St");
      new_name = new_name.replace("&", "");
      new_name = new_name.replaceAll(" ", "-");
      new_name = new_name.toLowerCase();
      return new_name + ".png";
    }
  };
</script>

<tr class="row" data-team={slugifyTeam(row.team)}>
  <th class="rank" scope="row">{row.currRank}</th>
  <td class="logo" aria-hidden="true">
    <img
      src={"https://graphics.axios.com/assets/sports-logos/college-logos/" +
        imgName(row.team)}
      width="20"
      height="20"
      alt=""
    />
  </td>
  <td class="team">
    {schoolName(row.team)}
    {#if row.firstPlace > 0}
      ({row.firstPlace})
    {/if}
  </td>
  <td class="record">{row.record}</td>
  <td class="points">{row.points}</td>
  <td class="trend">
    {#if row.change != 0}
      {#if row.change == "NR"}
        <span class="sr-only">Not ranked</span>
        <span aria-hidden="true">{row.change}</span>
      {:else if row.change > 0}
        <img
          src="https://graphics.axios.com/assets/sports-logos/college-logos/arrow-up.png"
          width="12"
          alt=""
          role="presentation"
        />
        <span><span class="sr-only">+</span>{row.change}</span>
      {:else}
        <img
          src="https://graphics.axios.com/assets/sports-logos/college-logos/arrow-down.png"
          width="12"
          alt=""
          role="presentation"
        />
        <span><span class="sr-only">-</span>{Math.abs(row.change)}</span>
      {/if}
    {:else}
      <span class="sr-only">No change</span>
      <span aria-hidden="true">-</span>
    {/if}
  </td>
</tr>

<style>
  .row {
    font-family: var(--font-nb-pro);
    line-height: 1.25;
    text-align: left;
    vertical-align: middle;
  }

  .row:not(:first-of-type) {
    border-top: 0.5px solid #cfd0d0;
  }

  td,
  th {
    padding: 8px 0;
    font-family: var(--font-nb-pro-mono);
    font-size: 13px;
    text-align: right;
    color: #333335;
    vertical-align: middle;
  }

  td + td,
  th + td {
    padding-left: var(--cell-spacing);
  }

  .rank {
    width: 25px;
  }

  .logo {
    text-align: center;
    width: 20px;
  }

  .logo img {
    display: block;
    margin: 0 auto;
    mix-blend-mode: multiply;
  }

  .team {
    font-family: var(--font-nb-pro);
    font-weight: bold;
    line-height: 1.25;
    text-align: left;
  }

  .record {
    width: 15%;
  }

  .trend {
    color: #898989;
    width: 17%;
  }

  .trend img {
    position: relative;
    left: 2px;
    opacity: 0.8;
  }

  /* .first-place {
      font-weight: normal;
    }
  
    .points {
      width: 20%;
    } */
</style>
