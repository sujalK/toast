<template>
  <div class="toast-widget" :class="widgetClass" v-if="show" id="custom-toaster">
    <div class="toast-icon" :class="background">
      <component :is="component" class="icon" />
    </div>
    <div class="text-area">
      <div class="toast-title">
        {{ toastTitle }}
      </div>
      <div class="toast-message-and-button">
        <span class="toast-message">
          {{ toastMessage }}
        </span>
        <span class="close-button" :class="buttonClass" @click="close">&times;</span>
      </div>
    </div>
  </div>
</template>
<script>
import IconSuccess from './Icons/IconSuccess.vue';
import IconWarning from './Icons/IconWarning.vue';
import IconError from './Icons/IconError.vue';

export default {
  emits: ['hide'],
  props: {
    show: {
      type: Boolean,
      default: false
    },
    title: {
      type: String,
    },
    message: {
      type: String
    },
    type: {
      type: String,
      default: 'success',
      validator(type) {
        return (typeof type === 'string') && (['success', 'error', 'warning'].includes(type));
      }
    }
  },
  components: {
    IconSuccess,
    IconWarning,
    IconError
  },
  data() {
    return {
      supportedTypes: ['success', 'error', 'warning'],
      timeout: null
    }
  },
  watch: {
    show(value) {
      if (value) {
        if (this.timeout) {
          clearTimeout(this.timeout);
        }

        this.timeout = setTimeout(() => {
          this.$emit('hide');
        }, 3000);

      } else {
        clearTimeout(this.timeout);
      }
    }
  },
  computed: {
    toastTitle() {
      if (this.supportedTypes.includes(this.title)) {
        return this.capitalizeFirstLetter(this.title);
      } else if (this.supportedTypes.includes(this.type)) {
        return this.capitalizeFirstLetter(this.type);
      }

      return 'Success';
    },
    toastMessage() {
      return this.message ? this.message : '';
    },
    propType() {
      return this.supportedTypes.includes(this.type) ? this.type : 'success';
    },
    component() {
      return `icon-${this.propType}`;
    },
    widgetClass() {
      return ['widget-bar-' + this.propType , this.propType + '-widget'];
    },
    background() {
      return `bg-${this.propType}`;
    },
    buttonClass() {
      return `${this.propType}-close-btn`;
    }
  },
  methods: {
    close() {
      this.$emit('hide');
    },
    capitalizeFirstLetter(data) {
      return data.charAt(0).toUpperCase() + data.slice(1);
    }
  }
}
</script>
<style scoped>
.toast-widget {
  position: relative;
  display: flex;
  align-items: center;
  gap: 20px;
  width: 300px;
  padding: 1rem 1rem;
  font-family: 'Lato', sans-serif;
  color: #555;
}

.toast-widget .toast-icon {
  color: #fff;
  border-radius: 50%;
}

.toast-widget .text-area {
  flex-grow: 1;
}

.toast-widget .text-area .toast-title {
  font-size: 1rem;
  line-height: 2.5;
  font-weight: bold;
}

.toast-widget .text-area .toast-message-and-button {
  position: relative;
  display: flex;
  align-items: center;
  gap: 20px;
}

.toast-widget .text-area .toast-message-and-button .toast-message {
  font-size: .8rem;
  line-height: 1.5;
}

.toast-widget .text-area .toast-message-and-button .close-button {
  position: absolute;
  top: -35px;
  right: 20px;
  cursor: pointer;
  font-size: 1.5rem;
}

.icon {
  width: 14px;
  height: 14px;
  padding: 0rem .2rem;
}

.success-widget:before {
  position: absolute;
  content: '';
  height: 100%;
  width: 4px;
  left: 0;
  background: #309438;
}

.warning-widget:before {
  position: absolute;
  content: '';
  height: 100%;
  width: 4px;
  left: 0;
  background: #f6b84c;
}

.error-widget:before {
  position: absolute;
  content: '';
  height: 100%;
  width: 4px;
  left: 0;
  background: #f23838;
}

.bg-success {
  background: #309438;
}

.success-close-btn {
  color: #7cc57c;
}

.widget-bar-success {
  background: #d9ffd9;
}

.bg-warning {
  background: #f6b84c;
}

.widget-bar-warning {
  background: #ffffab;
}

.warning-close-btn {
  color: #cbcb7a;
}

.bg-error {
  background: #ea9c9c;
}

.widget-bar-error {
  background: #ffdfdf;
}

.error-close-btn {
  color: #ea9c9c;
}
</style>