<template>
  <div class="modal is-active">
    <div class="modal-background"></div>
    <div
      class="modal-card"
      role="dialog"
      aria-labelledby="modalTitle"
      aria-describedby="modalDescription"
    >
      <header class="modal-card-head">
        <slot name="header">
          <p class="modal-card-title">new slot</p>
        </slot>
        <button class="delete" aria-label="close" @click="$emit('close')"></button>
      </header>

      <section class="modal-card-body">
        <article class="media-content">
          <slot name="body">
            <p>new slot</p>
          </slot>
        </article>
      </section>
    </div>
  </div>
</template>
