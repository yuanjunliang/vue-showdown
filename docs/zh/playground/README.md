---
sidebar: auto
---

# Playground :running:

## 输入你的 Markdown 代码

<textarea class="markdown-input" placeholder="在这里输入你的 Markdown 代码" :rows="rows" v-model="markdownText"/>

## 输出 HTML

<section class="markdown-output">
  <VueShowdown
    :markdown="markdownText"
    :options="options"
    :vue-template="props.vueTemplate"/>
</section>

## 设置 vue-showdown props

<ul class="vue-showdown-props">
  <li
    v-for="prop in Object.keys(props)"
    :key="prop"
  >
    <span>{{ prop }}</span>
    <input
      v-model="props[prop]"
      :type="typeof props[prop] === 'boolean' ? 'checkbox' : 'text'">
  </li>
</ul>

## 设置 showdown options

<ul class="showdown-options">
  <li v-for="opt in Object.keys(options)">
    <span>{{ opt }}</span>
    <input
      v-model="options[opt]"
      :type="typeof options[opt] === 'boolean' ? 'checkbox' : 'text'">
  </li>
</ul>

<script>
export default {
  data () {
    return {
      markdownText: `\
### Hello, Vue Showdown! :tada:

输入你的 Markdown 代码，立即得到相应的 HTML！

开启下面的 \`emoji\` 选项，启用 emoji 解析！ :smile:

开启下面的 \`vueTemplate\` Prop，启用 Vue 模板解析！

<span v-for="n in 5" :key="n" v-text="n"/>`,

      props: {
        vueTemplate: false,
      },

      options: {
        omitExtraWLInCodeBlocks: false,
        noHeaderId: false,
        prefixHeaderId: false,
        rawPrefixHeaderId: false,
        ghCompatibleHeaderId: false,
        rawHeaderId: false,
        headerLevelStart: false,
        parseImgDimensions: false,
        simplifiedAutoLink: false,
        excludeTrailingPunctuationFromURLs: false,
        literalMidWordUnderscores: false,
        literalMidWordAsterisks: false,
        strikethrough: false,
        tables: false,
        tablesHeaderId: false,
        ghCodeBlocks: true,
        tasklists: false,
        smoothLivePreview: false,
        smartIndentationFix: false,
        disableForced4SpacesIndentedSublists: false,
        simpleLineBreaks: false,
        requireSpaceBeforeHeadingText: false,
        ghMentions: false,
        ghMentionsLink: 'https://github.com/{u}',
        encodeEmails: true,
        openLinksInNewWindow: false,
        backslashEscapesHTMLTags: false,
        emoji: false,
        underline: false,
        completeHTMLDocument: false,
        metadata: false,
        splitAdjacentBlockquotes: false,
      },
    }
  },

  computed: {
    contentRows () {
      return this.markdownText.split('\n').length - 1
    },

    rows () {
      return this.contentRows < 3 ? 5 : this.contentRows + 2
    },
  }
}
</script>

<style lang="stylus" scoped>
@import '~@app/style/config.styl'

.markdown-input
  resize none
  outline none
  width 100%
  margin 15px 0
  padding 15px
  font-size 16px
  background-color #fdfdfd
  border 1px solid $borderColor
  border-radius 5px
  box-sizing border-box
  &:focus
    background-color #ffffff
    box-shadow 0 0 1px 1px lighten($accentColor, 50%)
  &::placeholder
    color $textLightColor
.markdown-output
  padding 10px 15px
  margin 15px 0
  background-color #fafbfc
  border 1px solid $borderColor
  border-radius 5px
</style>
