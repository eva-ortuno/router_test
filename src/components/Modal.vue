<template>
  <transition name="modal-fade">
    <div class="modal-backdrop">
      <div class="modal"
        role="dialog"
      >
        <header
          class="modal-header"
          id="modalTitle"
        >
          <slot name="header">
            Access Error!
          </slot>
          <button
            type="button"
            class="btn-close"
            @click="close"
            aria-label="Close modal"
          >
            x
          </button>
        </header>

        <section
          class="modal-body"
          id="modalDescription"
        >
          <slot name="body">
            You do not have the rights to access those tools. <br> Contact us for a free demo!
          </slot>
        </section>
      </div>
    </div>
  </transition>
</template>
<script>
  export default {
    name: 'Modal',
    methods: {
      close() {
        this.$emit('close')
      },
    },
  }
</script>

<style>
  .modal-backdrop {
    position: fixed;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    background-color: rgba(0, 0, 0, 0.3);
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .modal {
    background: #FFFFFF;
    overflow-x: auto;
    display: flex;
    flex-direction: column;
  }

  .modal-header {
    padding: 15px;
    display: flex;
    position: relative;
    border-bottom: 1px solid #eeeeee;
    color: #0063e4;
  }


  .modal-body {
    position: relative;
    padding: 20px 10px;
  }

  .btn-close {
    position: absolute;
    top: 0;
    right: 0;
    border: none;
    font-size: 20px;
    padding: 10px;
    cursor: pointer;
    font-weight: bold;
    color: #0063e4;
    background: transparent;
  }

  .modal-fade-enter,
  .modal-fade-leave-to {
    opacity: 0;
  }

  .modal-fade-enter-active,
  .modal-fade-leave-active {
    transition: opacity .5s ease;
  }
</style>