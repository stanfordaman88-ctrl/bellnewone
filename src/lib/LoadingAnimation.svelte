
<script>
  import { onMount } from 'svelte';
  import { push } from 'svelte-spa-router';

  let timeout;

  onMount(() => {
    timeout = setTimeout(() => {
      push('/login');
    }, 5000);

    return () => {
      clearTimeout(timeout);
    };
  });
</script>

<div class="loader-container">
  <div class="loader">
    <div class="dot"></div>
    <div class="dot"></div>
    <div class="dot"></div>
  </div>
</div>

<style>
  .loader-container {
    position: fixed;
    inset: 0;
    display: flex;
    align-items: center;
    justify-content: center;
    /* background: #111; */
    background: white;
    overflow: hidden;
  }

  .loader {
    position: relative;
    width: 160px;
    height: 160px;
    /* border: 4px solid #97e2dd; */
    border: 4px solid #003770;
    border-radius: 50%;
    animation: shadowOuter 4s ease-in-out infinite alternate;
  }

  .loader::before,
  .loader::after {
    content: '';
    position: absolute;
    top: 50%;
    left: 50%;
    box-sizing: border-box;
    border-radius: 50%;
    transform: translate(-50%, -50%);
  }

  .loader::before {
    width: 152px;
    height: 152px;
    border: 3px solid rgba(51, 86, 150, 0.75);
    animation: shadowInner 4s ease-in-out infinite alternate;
  }

  .loader::after {
    width: 146px;
    height: 146px;
    border: 3px solid rgba(51, 86, 150, 0.25);
    filter: drop-shadow(0 0 14px #335696);
  }

  .dot {
    position: absolute;
    top: 50%;
    width: 20px;
    height: 20px;
    overflow: visible;
    transform: rotate(0deg);
    transition: all 1s ease;
  }

  .dot::after {
    content: '';
    position: absolute;
    top: -4px;
    left: 8px;
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: #003770;
    filter:
      drop-shadow(0 0 4px #97e2dd)
      drop-shadow(0 0 2px #335696);
  }

  .dot:nth-child(1) {
    left: calc(33% - 10px);
    animation: moveFirst 2s ease infinite;
  }

  .dot:nth-child(2) {
    left: calc(50% - 10px);
    animation: moveSecond 2s ease infinite;
  }

  .dot:nth-child(3) {
    left: calc(67% - 10px);
    animation: moveThird 2s ease infinite;
  }

  @keyframes moveFirst {
    from {
      left: calc(33% - 10px);
    }
    to {
      left: calc(50% - 10px);
    }
  }

  @keyframes moveSecond {
    from {
      left: calc(50% - 10px);
    }
    to {
      left: calc(67% - 10px);
    }
  }

  @keyframes moveThird {
    0% {
      left: calc(67% - 10px);
      transform: rotate(0deg);
    }
    100% {
      left: calc(33% - 10px);
      transform: rotate(360deg);
    }
  }

  @keyframes shadowOuter {
    from {
      filter: drop-shadow(0 0 4px #335696);
    }
    to {
      filter: drop-shadow(0 0 12px #335696);
    }
  }

  @keyframes shadowInner {
    from {
      filter: drop-shadow(0 0 12px #335696);
    }
    to {
      filter: drop-shadow(0 0 20px #335696);
    }
  }

  @media (prefers-reduced-motion: reduce) {
    .loader,
    .loader::before,
    .dot {
      animation-duration: 8s;
    }
  }
</style>
