<template>
  <div id="wps-viewer-service" />
</template>

<script>
export default {
  name: 'wps-viewer-service',
  methods: {
    /**
     * 重置
     */
    _reload ({ token, wpsUrl }) {
      let wps_inc = WPS.config({
        wpsUrl,
        mount: document.querySelector('#wps-viewer-service')
      })
      wps_inc.setToken({ token })
    }
  },
  created () {
    window.addEventListener('message', ({ data }) => {
      if (data.type === 'WPS_VIEWER_SERVICE') {
        this._reload(event.data)
      }
    }, false)
  }
}
</script>

<style lang="scss">
  html, body{
    width: 100%;
    height: 100%;
  }
  #wps-viewer-service {
    height: 100%;
    iframe {
      width: 100%;
      height: 100%;
    }
  }
</style>
