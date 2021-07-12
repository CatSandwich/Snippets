<template>
  <pre v-highlightjs="html" :class="lang"><code class="d-block overflow-auto p-1"/></pre>
</template>

<script>
export default{
  props: {
    link: String,
    start: Number,
    end: Number,
    content: String,
    lang: String
  },
  data: () => ({
    html: ''
  }),
  created(){
    if(this.link){
      fetch(this.link)
          .then(res => res.text())
          .then(text => text.split('\n'))
          .then(lines => this.html = lines.slice(this.start - 1 || 0, this.end || lines.length).join('\n'));
    }
    else{
      this.html = this.content || '';
    }
  }
}
</script>
