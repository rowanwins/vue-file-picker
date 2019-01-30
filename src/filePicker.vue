<template>
  <div
    :id="id"
    class="vfp"
  >
    <div
      class="vfp-bgArea"
      :class="{ 'vfp-active': isActive }"
      @dragover="setActive"
      @dragleave="cancelActive"
      @drop="fileAdded"
    >
      <div class="vfp-iconHolder vfp-gridItem">
        <slot name="icon" />
      </div>
      <input
        id="vfp-filePicker"
        class="vfp-inputfile vfp-gridItem"
        type="file"
        name="vfp-filePicker"
        :accept="accept"
        :multiple="allowMultiple"
        @change="fileAdded"
      >
      <label
        class="vfp-label vfp-gridItem"
        for="vfp-filePicker"
      >
        <slot name="label">
          <strong>Choose a file</strong> or drop it here
        </slot>
      </label>
    </div>
  </div>
</template>

<script>
export default {
  name: 'FilePicker',
  props: {
    id: {
      type: String,
      required: true,
      default: 'filePicker'
    },
    accept: {
      type: String,
      default: '*/*'
    },
    allowMultiple: {
        type: Boolean,
        default: false
    }
  },
  data: function () {
    return {
        isActive: false
    }
  },
  computed: {
    requiresTypeCheck: function () {
      return this.accept !== '*/*'
    },
    acceptedTypes: function () {
      return this.accept.split(',')
    }
  },
  methods: {
    cancelHandlers (e) {
        e.preventDefault()
        e.stopPropagation()
    },
    setActive (e) {
        this.isActive = true
        this.cancelHandlers(e)
    },
    cancelActive (e) {
        this.isActive = false
        this.cancelHandlers(e)
    },
    fileAdded (e) {
        this.isActive = false
        this.cancelHandlers(e)
        const wasDropped = e.dataTransfer
        const files = wasDropped ? e.dataTransfer.files : e.target.files

        if (wasDropped && !this.allowMultiple && files.length > 1) throw new Error('vue-file-picker: Multiple Files are not allowed')

        if (wasDropped && this.requiresTypeCheck) {
          for (var i = 0; i < files.length; i++) {
            if (this.acceptedTypes.indexOf(files[i].type) === -1) throw new Error('vue-file-picker: File type not allowed')
          }
        }
        this.$emit('vfp-file-added', files)
    }
  }
}
</script>

<style lang="scss">

.vfp {
    display: flex;
    height: 100px;

    .vfp-bgArea {
        transition: 0.3s;
        background: #F2F3F4;
        display: grid;
        grid-template-rows: 60% 40%;
        padding: 25px 10px;
        width: 100%;
        outline: 2px dashed #CACFD2;
        outline-offset: -10px;
        color: #3b3e40;
        text-align: center;
    }

    .vfp-inputfile {
        width: 0.1px;
        height: 0.1px;
        opacity: 0;
        overflow: hidden;
        position: absolute;
    }

    .vfp-gridItem {
        align-self: center;
        justify-self: center;
    }

    .vfp-label {
        cursor: pointer;
        text-align: center;
        font-size: 0.9rem;
    }

    .vfp-active {
        background-color: #D7DBDD;
        outline-color: #F2F3F4;
    }

    @media only screen and (max-width: 440px) {
        .vfp-bgArea {
            padding: 18px 10px;
            grid-template-rows: 50% 50%;
            grid-row-gap: 5px;
        }
    }
}

</style>
