<script lang="ts">
  export let links = [
    { name: 'Pricing', url: '/pricing' },
    { name: 'Help', url: '/help' },
  ];
</script>

<div class="header-wrapper">
  <header class="header">
    <div class="header__container">
      <a href="/" class="header__logo" aria-label="Homepage">
        <img src="/icons/logo.png" width="50" alt="logo">
        <span class="header__logo-text">Ourocon</span>
      </a>
      <div class="header__nav-scroller">
        <nav class="header__nav" aria-label="Primary">
          <ul class="header__nav-list">
            {#each links as link}
              <li class="header__nav-item">
                <a href={link.url} class="header__nav-link">{link.name}</a>
              </li>
            {/each}
          </ul>
        </nav>
      </div>
      <div class="header__actions">
        <a href="/login" class="header__action header__action--secondary">Log In</a>
        <a href="/signup" class="header__action header__action--primary">Get Started</a>
      </div>
    </div>
  </header>
</div>

<style lang="scss">
  @use '../../../styles/global.scss';

  .header-wrapper {
    container-type: inline-size;
  }

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
    gap: var(--space-md);
  }

  .header__logo {
    display: flex;
    align-items: center;
    gap: var(--space-sm);
    font-weight: 700;
    font-size: 1.25rem;
    color: var(--c-text);
    text-decoration: none;
    transition: all var(--transition-fast);

    &:hover {
      text-decoration: none;
    }

    svg {
      color: var(--c-primary);
      flex-shrink: 0;
    }
  }

  .header__nav-scroller {
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none; /* Firefox */
    &::-webkit-scrollbar {
      display: none; /* Safari and Chrome */
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
    white-space: nowrap;

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
    white-space: nowrap;

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

  /* Shape C: Expanded (Default) */
  @container (width >= 961px) {
    .header__nav-scroller {
      overflow-x: visible;
    }
  }

  /* Shape B: Condensed */
  @container (481px < width < 961px) {
    .header__container {
      gap: var(--space-sm);
    }
    .header__logo-text {
      font-size: 1rem;
    }
    .header__action--secondary {
      @media (width < 520px) {
        display: none;
      }
    }
  }

  /* Shape A: Compact */
  @container (width <= 480px) {
    .header__container {
      flex-wrap: wrap;
      gap: var(--space-sm);
    }
    .header__logo-text {
      display: none;
    }
    .header__nav-scroller {
      order: 3;
      width: 100%;
    }
    .header__actions {
      margin-left: auto;
    }
    .header__action--secondary {
      display: none;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .header__logo,
    .header__action {
      transition: none;
    }
  }
</style>
