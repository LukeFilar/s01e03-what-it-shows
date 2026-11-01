<script lang="ts">
  import reports from '#lib/data/reports-4471.json';
  import { causeOf, uniqueById, type Report } from '#lib/kb/causes';
  import { tenantOf } from '#lib/kb/locales';

  let { ticket }: { ticket: number } = $props();

  // One problem per row, counted the way the desk's cause table counts them.
  const rows = $derived.by(() => {
    const merged = uniqueById(reports as Report[]).filter((r) => r.mergedInto === ticket);
    const count = { parser: 0, hint: 0, other: 0 };
    for (const r of merged) {
      const cause = causeOf(r, tenantOf(r));
      if (cause) count[cause]++;
      else count.other++;
    }
    return [
      { problem: 'Shared parser reads dates month first', reports: count.parser },
      { problem: 'booking-v3 form hints MM/DD/YYYY to day-first tenants', reports: count.hint },
      { problem: 'Not placed', reports: count.other },
    ].filter((row) => row.reports > 0);
  });
  const total = $derived(rows.reduce((n, row) => n + row.reports, 0));
</script>

<table>
  <thead><tr><th>problem</th><th>reports</th></tr></thead>
  <tbody>
    {#each rows as row (row.problem)}
      <tr><td>{row.problem}</td><td>{row.reports}</td></tr>
    {/each}
  </tbody>
  <tfoot><tr><th>merged into #{ticket}</th><th>{total}</th></tr></tfoot>
</table>
