<script lang="ts">
  import reports from '#lib/data/reports-4471.json';
  import notes from '#lib/data/desk-notes.json';
  import { causeOf, uniqueById, type Report } from '#lib/kb/causes';
  import { tenantOf } from '#lib/kb/locales';

  let { ticket }: { ticket: number } = $props();

  // One problem per row. The five reports the desk read as a one-day move are their own problem,
  // not part of `parser`, even though causes.ts files them there by tenant.
  const rows = $derived.by(() => {
    const merged = uniqueById(reports as Report[]).filter((r) => r.mergedInto === ticket);
    const count = { parser: 0, hint: 0, oneDay: 0, other: 0 };
    for (const r of merged) {
      if (notes.oneDayMove.includes(r.id)) count.oneDay++;
      else {
        const cause = causeOf(r, tenantOf(r));
        if (cause) count[cause]++;
        else count.other++;
      }
    }
    return [
      { problem: 'Shared parser reads dates month first', reports: count.parser },
      { problem: 'booking-v3 form hints MM/DD/YYYY to day-first tenants', reports: count.hint },
      { problem: 'Date lands one day off (not a month/day flip)', reports: count.oneDay },
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
