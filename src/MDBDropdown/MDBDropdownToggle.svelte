<script>
  import { getContext } from 'svelte';

  import { clean, clsx } from '../utils';

  import MDBBtn from '../Btn/MDBBtn.svelte';

  const context = getContext('dropdownContext');

  let className = '';
  export { className as class };
  export let caret = false;
  export let color = 'secondary';
  export let disabled = false;
  export let ariaHaspopup = true;
  export let ariaLabel = 'Toggle Dropdown';
  export let split = false;
  export let nav = false;
  export let size = '';
  export let tag = null;
  export let outline = false;

  const props = clean($$props);

  $: classes = clsx(className, {
    'dropdown-toggle': caret || split,
    'dropdown-toggle-split': split,
    'nav-link': nav
  });

  function toggleMDBBtn(e) {
    if (disabled) {
      e.preventDefault();
      return;
    }

    if (nav) {
      e.preventDefault();
    }

    $context.toggle(e);
  }
</script>

{#if nav}
  <a
    {...props}
    on:click
    on:click={toggleMDBBtn}
    href="#nav"
    {ariaHaspopup}
    class={classes}>
    <slot>
      <span class="sr-only">{ariaLabel}</span>
    </slot>
  </a>
{:else if tag === 'span'}
  <span
    {...props}
    on:click
    on:click={toggleMDBBtn}
    {ariaHaspopup}
    class={classes}
    {color}
    {size}>
    <slot>
      <span class="sr-only">{ariaLabel}</span>
    </slot>
  </span>
{:else}
  <MDBBtn
    {...props}
    on:click={toggleMDBBtn}
    {ariaHaspopup}
    class={classes}
    {color}
    {size}
    {outline}>
    <slot>
      <span class="sr-only">{ariaLabel}</span>
    </slot>
  </MDBBtn>
{/if}
