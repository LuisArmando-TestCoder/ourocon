<script lang="ts">
  export let links = [
    { name: 'Pricing', url: '/pricing' },
    { name: 'Help', url: '/help' },
  ];
</script>

<header class="header">
  <div class="header__container">
    <a href="/" class="header__logo" aria-label="Homepage">
      <svg width="40" height="40" viewBox="0 0 100 100" fill="none" xmlns="http://www.w3.org/2000/svg"><rect width="100" height="100" rx="20" fill="currentColor"/></svg>
      <span class="header__logo-text">Ourocon</span>
    </a>
    <nav class="header__nav" aria-label="Primary">
      <ul class="header__nav-list">
        {#each links as link}
          <li class="header__nav-item"><a href={link.url} class="header__nav-link">{link.name}</a></li>
        {/each}
      </ul>
    </nav>
    <div class="header__actions">
      <a href="/login" class="header__action header__action--secondary">Log In</a>
      <a href="/signup" class="header__action header__action--primary">Get Started</a>
    </div>
  </div>
</header>

<style lang="scss">
  @use '../../../styles/global.scss';

  .header {
    background: var(--c-bg);
    padding: var(--space-md) 0;
    border-bottom: 1px solid var(--c-border);
    position: relative;
    z-index: 1000;
  }

  .header__container {
    display: flex;
    justify-content: space-between;
    align-items: center;
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 var(--space-md);
  }

  .header__logo {
    display: flex;
    align-items: center;
    gap: var(--space-sm);
    font-weight: 700;
    font-size: 1.25rem;
    color: var(--c-text);
    text-decoration: none;

    &:hover {
      text-decoration: none;
    }

    svg {
      color: var(--c-primary);
    }
  }

  .header__nav-list {
    list-style: none;
    margin: 0;
    padding: 0;
    display: flex;
    gap: var(--space-lg);
  }

  .header__nav-link {
    color: var(--c-text-light);
    font-weight: 500;
    text-decoration: none;

    &:hover {
      color: var(--c-primary);
    }
  }

  .header__actions {
    display: flex;
    align-items: center;
    gap: var(--space-sm);
  }

  .header__action {
    padding: var(--space-sm) var(--space-md);
    border-radius: var(--radius-md);
    text-decoration: none;
    font-weight: 600;
    transition: all var(--transition-fast);

    &--primary {
      background-color: var(--c-primary);
      color: var(--c-white);
      border: 1px solid var(--c-primary);
      &:hover {
        background-color: var(--c-white);
        color: var(--c-primary);
      }
    }

    &--secondary {
      background-color: var(--c-bg);
      color: var(--c-primary);
      border: 1px solid var(--c-border);
      &:hover {
        border-color: var(--c-primary);
      }
    }
  }
</style>
