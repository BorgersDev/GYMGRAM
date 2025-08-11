<script setup>

    defineProps({
        handleCloseModal: Function
    })
</script>

<template>
  <Teleport to="#portal">
    <div class="portal-container">
      <!-- underlay cobre a tela, blur + escurecido -->
      <div role="button" tabindex="0" @click="handleCloseModal" class="portal-underlay"></div>

      <!-- conteúdo branco por cima -->
      <div class="portal-content">
        <slot />
      </div>
    </div>
  </Teleport>
</template>

<style scoped>
.portal-container {
  position: fixed;
  inset: 0;
  z-index: 1000;
}

/* desfoca o que está atrás e escurece levemente sem usar opacity */
.portal-underlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.35);   /* “escurecido” */
  backdrop-filter: blur(2px);
  -webkit-backdrop-filter: blur(6px); /* suporte Safari */
  z-index: 1;
}

/* card central branco, intacto */
.portal-content {
  position: absolute;
  z-index: 2;                        /* acima do underlay */
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  width: 600px;
  max-width: 90vw;
  max-height: 80vh;
  overflow: auto;
  display: grid;
  place-items: center;
  background: var(--background-primary);      
  opacity: 0.8;            /* branco puro */
  border-radius: var(--border-radius-small);
  padding: 1rem;
  border: 1px solid var(--background-muted);
  box-shadow: 0 20px 40px rgba(0,0,0,.25);
}
</style>
