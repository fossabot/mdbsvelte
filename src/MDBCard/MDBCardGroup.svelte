<script>

  import { clean, clsx } from '../utils';

  let className = '';
  export { className as class };

  const props = clean($$props);

  $: classes = clsx(className, 'card-group');
</script>

<div {...props} class={classes}>
  <slot />
</div>
