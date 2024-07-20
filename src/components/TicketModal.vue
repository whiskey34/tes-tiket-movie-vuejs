<script>
export default {
  props: ['movie'],
  computed: {
    qrCodeUrl() {
      // Generate the QR code URL using a QR code generation API
      return `https://api.qrserver.com/v1/create-qr-code/?data=${encodeURIComponent(this.movie.id)}&size=200x200`;
    }
  },
};
</script>

<template>
    <div class="modal-overlay">
        <div class="modal-content">
            <button class="modal-close" @click="$emit('close')">×</button>
            <div class="modal-body">
                <h3 class="2xl font-bold">Purchase Ticket</h3>
                <p class="mb-3">Scan this QR Code to buy ticket for this movie.</p>
                <div class="barcode-container text-center items-center mt-2">
                    <img :src="qrCodeUrl" alt="Barcode" />
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.5);
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  width: 80%;
  max-width: 500px;
  position: relative;
}

.modal-close {
  position: absolute;
  top: 10px;
  right: 10px;
  background: transparent;
  border: none;
  font-size: 20px;
  cursor: pointer;
}

/* .barcode-container {
  text-align: center;
  margin-top: 20px;
}

.barcode-container img {
  max-width: 100%;
} */
</style>