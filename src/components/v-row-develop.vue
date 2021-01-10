<template>
  <div>
      <div class="DevRow">
        <select v-model="font" class="form-select" aria-label="Default select example">
        <option value="Arial, sans-serif" selected >Arial, sans-serif</option>
        <option value="Arial Narrow, sans-serif">Arial Narrow, sans-serif</option>
        <option value="Impact, fantasy">Impact, fantasy</option>
        <option value="Palatino, URW Palladio L, serif">Palatino, URW Palladio L, serif</option>
        <option value="Courier New, monospace">Courier New, monospace</option>
        <option value="Mistral"> Mistral</option>
        <option value="Times New Roman">Times New Roman</option>
        </select>
        <button title="назад по действию"  class="btnD BackAct btn btn-light" @click="Undo">
          <img id="backActImg" src="../assets/VectorBackAct.png" alt="">
        </button>
        <button title="вперед по действию" class="btnD RepeatAct btn btn-light"  @click="Redo">
          <img class="RepeatActImg" src="../assets/VectorRepeatAct.png" alt="">
        </button>
        <button title="Сделать выделенный текст заголовком" class="btnD TitleT btn btn-light" @click="ToHead">
          <img class="TitleImg" src="../assets/VectorTitleT.png" alt="">
        </button>
        <button title="Сделать выделенный текст абзацом" @click="ToParagraph" class="btnD Paragraph btn btn-light">
          <img class="ParagraphImg1" src="../assets/VectorParagraph.png" alt="">
          <img class="ParagraphImg2" src="../assets/VectorParagraph.png" alt="">
        </button>
        <button title="Вставить картинку на место курсора" @click="PasteImgM" class="btnD PasteImgBlock btn btn-light">
          <img class="PasteImg" src="../assets/VectorPasteImg.png" alt="">
        </button >
        <button @click="MakeItalicM" class="MakeItalicB btnD btn btn-light">
          <img class="MakeItalic" src="../assets/icons8-курсив-40.png" alt="">
        </button>
        <button @click="MakeTireM" class="MakeTireB btnD btn btn-light">
          <img class="MakeTire" src="../assets/icons8-зачеркивание-30.png" alt="">
        </button>
        <button @click="SetFontM" class="SetFontB btnD btn btn-light">
          <img class="SetFont" src="../assets/icons8-текст-64.png" alt="">
        </button>
        <input v-model="fsize" class="setPix" value="16 px'">
        <a title="скопировать html-код страницы"  v-clipboard="htmlcodea" @click="CopyHtml" class="CopyHtml" href="#">
          Скопировать HTML
        </a>
      </div>
      <div class="TextAreaBlock">
        <div ref="txtarea" class="textArea" >
          <p :style="{'font-size' : fsize + 'px'}"  id="area" ref="TextP" class="BordenUp" contenteditable="true" placeholder="Здесь вы можете начать свой документ"></p>
        </div>
      </div>
  </div>
</template>

<script>
export default {
  mounted () {
    this.text = this.$refs.PText
  },
  data () {
    return {
      fsize: '16',
      tabT: '&nbsp;&nbsp;&nbsp;&nbsp;',
      dnshow: 'false',
      htmlcodea: '<!DOCTYPE html> <html lang="en">  <head>    <meta charset="utf-8">    <meta http-equiv="X-UA-Compatible" content="IE=edge">    <meta name="viewport" content="width=device-width,initial-scale=1.0">    <link rel="icon" href="<%= BASE_URL %>favicon.ico">    <title><%= htmlWebpackPlugin.options.title %></title>  </head>  <body>    <noscript>      <strong>Were sorry but <%= htmlWebpackPlugin.options.title %> doesn t work properly without JavaScript enabled. Please enable it to continue.</strong>    </noscript>    <div id="app"></div>    <!-- built files will be auto injected -->  </body></html>)',
      start: 0,
      end: 0,
      font: '',
      ttt: 'Таким образом консультация с широким активом представляет собой интересный эксперимент проверки позиций, занимаемых участниками в отношении поставленных задач. С другой стороны постоянное информационно-пропагандистское обеспечение нашей деятельности представляет собой интересный эксперимент проверки форм развития. Идейные соображения высшего порядка, а также укрепление и развитие структуры влечет за собой процесс внедрения и модернизации соответствующий условий активизации. Задача организации, в особенности же реализация намеченных плановых заданий играет важную роль в формировании дальнейших направлений развития. Повседневная практика показывает, что постоянное информационно-пропагандистское обеспечение нашей деятельности играет важную роль в формировании существенных финансовых и административных условий.'
    }
  },
  components: {
  },
  methods: {
    SetFS () {
      console.log('called')
      this.fsize = this.fsize.substring(0, this.fsize.length - 2)
    },
    SetFontM () {
      this.$refs.txtarea.focus()
      document.execCommand('fontName', false, this.font)
    },
    MakeTireM () {
      this.$refs.txtarea.focus()
      document.execCommand('strikeThrough')
    },
    MakeItalicM () {
      this.$refs.txtarea.focus()
      document.execCommand('italic')
    },
    CopyHtml () {
      return this.htmlcode
    },
    PasteImgM () {
      const a = prompt()
      this.$refs.txtarea.focus()
      if (a !== null) {
        if (document.execCommand('insertImage', false, a)) {

        }
      }
    },
    Undo () {
      this.$refs.txtarea.focus()
      document.execCommand('undo')
    },
    Redo () {
      this.$refs.txtarea.focus()
      document.execCommand('redo')
    },
    ToHead () {
      document.execCommand('fontsize', true, 4)
    },
    ToParagraph () {
      this.$refs.txtarea.focus()
      document.execCommand('indent')
    }
  }
}

</script>

<style>
.setPix:active, .setPix:focus {
outline: none
}
.setPix{
border: none;
position: absolute;
width: 42px;
height: 38px;
left: 535px;
top: 42px;
border-radius: 4px;
background: rgb(154, 165, 165);
}
.SetFont{
  position: absolute;
  width: 27px;
  top: 17%;
  left: 20%;
}
.SetFontB{
border: none;
position: absolute;
width: 42px;
height: 38px;
left: 482px;
top: 77px;
background: #282828;
border-radius: 4px;
}
.form-select{
  position: absolute;
  left: 535px;
  background: rgb(154, 165, 165);
  top:6%;
}
.MakeTire{
 position: absolute;
  left:20%;
  top: 20%;
  width: 24px;
}
.MakeTireB{
  border: none;
position: absolute;
width: 42px;
height: 38px;
left: 429px;
top: 77px;
background: #282828;
border-radius: 4px;
}
.MakeItalic{
  position: absolute;
  left:20%;
  top: 20%;
  width: 24px;
}
.MakeItalicB{
  border: none;
position: absolute;
width: 42px;
height: 38px;
left: 376px;
top: 77px;
background: #282828;
border-radius: 4px;
}
[contenteditable=true]:empty:before{
  content: attr(placeholder);
  pointer-events: none;
}
.btnD:active, .btnD:focus{
outline-color: rgb(20, 96, 211);
}
img{
   height: auto;
    width: auto;
    max-width: 500px;
    max-height: 500px;
  display: block;
  margin-left: auto;
  margin-right: auto;
}
span{
-moz-user-select: -moz-none;
-o-user-select: none;
-khtml-user-select: none;
-webkit-user-select: none;
user-select: none;
}
.BordenUp:active, .BordenUp:focus {
outline: none
}
.BordenUp{
  min-height: 800px;
  border: none;
}
.textArea{
  min-height: 984px;;
  border: none;
  font-family: 'Roboto', sans-serif;
  border-color: rgb(48, 44, 44) ;
  width: 746px;
  background-color: #282828;
  color: white;
}
.TextAreaBlock{
position: absolute;
width: 621px;
height: 253px;
left: 107px;
top: 146px;

font-family: Roboto;
font-style: normal;
font-weight: normal;
font-size: 15px;
line-height: 23px;
/* or 153% */
color: #EAEAEA;
}
.CopyHtml{
position: absolute;
width: 137px;
height: 23px;
left: 784px;
top: 85px;
font-family: 'Roboto', sans-serif;
font-style: normal;
font-weight: normal;
font-size: 15px;
line-height: 23px;
color: #639EFF;
}
.PasteImg{
position: absolute;
left: 20.69%;
right: 50.02%;
top: 24.22%;
bottom: 92.35%;
}
.PasteImgBlock{
border:none;
position: absolute;
width: 42px;
height: 38px;
left: 323px;
top: 77px;

background: #282828;
border-radius: 4px;
}
.ParagraphImg1{
  position: absolute;
left: 18.14%;
right: 51.83%;
top: 28.79%;
bottom: 21.65%;
}
.ParagraphImg2{
position: absolute;
left: 50.11%;
right: 3.86%;
top: 28.79%;
bottom: 21.65%;
}
.Paragraph{
  border: none;
  position: absolute;
width: 42px;
height: 38px;
left: 269px;
top: 77px;

background: #282828;
border-radius: 4px;
}
.TitleImg{
  position: absolute;
left: 26.19%;
right: 87.54%;
top: 20.29%;
bottom: 92.27%;
}
.TitleT{
  border: none;
  position: absolute;
width: 42px;
height: 38px;
left: 215px;
top: 77px;

background: #282828;
border-radius: 4px;
}
#backActImg{
  position: absolute;
left: 20.19%;
right: 85.54%;
top: 20.29%;
bottom: 92.27%;

}
.BackAct{
  border: none;
  position: absolute;
width: 42px;
height: 38px;
left: 107px;
top: 77px;

background: #282828;
border-radius: 4px;
}
.RepeatAct{
  border: none;
position: absolute;
width: 42px;
height: 38px;
left: 161px;
top: 77px;

background: #282828;
border-radius: 4px;
}
.RepeatActImg{
  position: absolute;
left: 20.09%;
right: 77.64%;
top: 20.29%;
bottom: 92.27%;

}
</style>
