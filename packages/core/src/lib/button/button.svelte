<!--
@component
  
For user triggered actions.

```svelte
<Button type="submit" variant="success" on:click={onClick} />
```
-->
<svelte:options immutable />

<script lang="ts">
import cx from 'classnames';
import { Icon } from '$lib';

/** Whether or not the button accepts clicks. */
export let disabled = false;

/** The behavior of the button. */
export let type: 'button' | 'submit' | 'reset' = 'button';

/** The communicated action type to the user. */
export let variant:
  | 'primary'
  | 'inverse-primary'
  | 'ghost'
  | 'danger'
  | 'outline-danger'
  | 'success' = 'primary';

/** The text displayed. */
export let label = '';

/** The text that appears in a popup box when mouse is over the element. */
export let title = '';

/**
 * The icon shown in the button.
 */
export let icon = '';

/** The width of the button. */
export let width: 'full' | 'default' = 'default';
</script>

<button
  {type}
  aria-disabled={disabled}
  {disabled}
  {title}
  class={cx(
    'mx-auto inline-flex items-center justify-center gap-1.5 whitespace-nowrap border py-1.5 text-xs',
    {
      'pointer-events-none select-none !border-disabled-light !bg-disabled-light text-disabled-dark':
        disabled,
      'flex w-full': width === 'full',
      'inline-flex': width !== 'full',
      'px-3': !icon,
      'pl-2 pr-3': icon,
      'border-light bg-light hover:border-medium hover:bg-medium active:bg-gray-2':
        variant === 'primary',
      'border-gray-9 bg-gray-9 text-white hover:border-black hover:bg-black active:bg-[#000]':
        variant === 'inverse-primary',
      'active-border-[rgba(0,0,0,0.08)] border-transparent hover:bg-[rgba(0,0,0,0.04)] active:bg-[rgba(0,0,0,0.08)]':
        variant === 'ghost',
      'border-danger-dark bg-danger-dark text-white hover:bg-[#aa2a2b] active:bg-[#9e2728]':
        variant === 'danger',
      'border-success-dark bg-success-dark text-white': variant === 'success',
      'border-danger-medium bg-danger-light text-danger-dark hover:bg-[#f5dfdc] active:bg-[#f6d7d3]':
        variant === 'outline-danger',
    }
  )}
  style={disabled ? '-webkit-user-select: none' : ''}
  on:click
>
  {#if icon}
    <span
      class={cx({
        'text-gray-6': variant === 'primary',
        'text-gray-4': disabled,
      })}
    >
      <Icon name={icon} />
    </span>
  {/if}

  <span>
    {label}
  </span>
</button>