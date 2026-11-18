<script lang="ts" generics="T extends string, U extends T">
  let {
    value = $bindable(),
    options,
    borderStyle,
  }:{
    value: T
    options: U[],
    borderStyle?: "left" | "bottom"
  } = $props();

  function format(s: string): string {
  const spaced = s
    .replace(/(?<=[a-z0-9])(?=[A-Z])|(?<=[a-zA-Z])(?=\d)/g, " ")
    .toLowerCase();
  return spaced.charAt(0).toUpperCase() + spaced.slice(1);
}

  const id = $props.id()
</script>



<div class="tabs">
  {#each options as option}
    <label class="tab">
      <input 
        type="radio" 
        name="tabs-{id}" 
        value={option}
        bind:group={value}
      >
      <span 
        class="tabLabel"
        class:borderLeft={borderStyle === "left"}
        class:borderBottom={borderStyle === "bottom"}
      >
        {format(option)}
      </span>
    </label>
  {/each}
</div>

<style>
  .tabs {
    padding: var(--standard-padding);
    display: inline-flex;
    gap: var(--tabs-gap, var(--standard-padding));
    justify-content: var(--justify-content, flex-start);
    flex-direction: var(--flex-direction, row);
    align-items: var(--align-items, start);
  }
  .tabLabel {
    display: inline-block;
    padding: var(--standard-padding);
  }
  .tab{
    position: relative;
  }
  .tab:first-child{
    left: var(--first-child-padding, calc(-1 * var(--standard-padding)));
  }
  .tab input:checked + .tabLabel {
    background: var(--gray3);
    color: var(--gray0);
  }
  .borderLeft{ border-left: var(--border-width) solid var(--gray3) }
  .borderBottom{ border-bottom: var(--border-width) solid var(--gray3) }
</style>