<script>
  function toggleMobileMenu() {
    const button = document.getElementById("mobile-menu-button");
    const menu = document.getElementById("menu-content");
    if (!button || !menu) return;
    const expanded = button.getAttribute("aria-expanded") === "true";
    button.setAttribute("aria-expanded", !expanded);
    menu.setAttribute("aria-expanded", !expanded);
  }
</script>

<div id="menu" class="menu mobile">
  <button
    id="mobile-menu-button"
    class="hamburger"
    aria-label="Abrir menu"
    aria-expanded="false"
    aria-controls="mobile-menu"
    type="button"
    onclick={toggleMobileMenu}
  >
    <span class="hamburger-icon">
      <span class="line top"></span>
      <span class="line middle"></span>
      <span class="line bottom"></span>
    </span>
  </button>
  <div id="menu-content" class="menu-content" aria-expanded="false">
    <a href="/">Aulas</a>
    <a href="/about">Sobre</a>
    <a href="/politicas-de-privacidade">Privacidade</a>
  </div>
</div>
