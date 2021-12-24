<template>
  <div id="app">
 <div class = "wrapper">
        <div id = "app">
            <div class = "left">
               <div class = "left_top" v-for = '(item, index) in items' :key="index">
                    <a href="#"  class = "lefta"  @click.prevent = 'editText(index)'> {{item.data}}</a>
                </div>
                <span class = "lefts" @click = 'activeNotepad=true'>Новый</span>
            </div>
 
            <div class = "right">
                <span class = "rights">Notepad++</span>
                <textarea  class = "righttext" cols = "50" rows = "20" v-model = 'newItem' v-if = 'activeNotepad' @keydown.ctrl.enter = 'addItem()' ></textarea>
                <textarea class = "righttext" cols = "50" rows = "20" v-if = '!activeNotepad' v-model = 'items[newIndex].text' @keydown.esc = 'del(newIndex)'></textarea>
                <div class = "right_bottom"> <span style = "font-size: 30px"> Ctrl+Enter</span>= сохранить, <span style = "font-size: 30px"> Esc</span>=удалить.</div>
            </div>
        </div>
        </div>
  </div>
</template>
<script>
 function addZero(date){
        if(date >= 0 && date <= 9){
            return '0' + date;
        }
        return date;
    }

export default {
  name: 'App',
  data () {
    return {
       activeNotepad:true,
        newItem:'',
        newIndex:'',
        items:[
            {text:'Hello world!', data:'2021.12.24 14:00:00'},
        ],
    }
  },
   methods:{
            del:function(elem){
                let delet = confirm('Удалить событья?');
                if(delet){
                    this.activeNotepad = true;
                    this.items.splice(elem, 1);
                }
            },
            editText:function(index){
                this.activeNotepad = false;
                this.newIndex = index;  
            },
            addItem:function(){
                if(!(this.newItem == '')){
                    let date = new Date();
                    let year = date.getFullYear();
                    let month = date.getMonth() + 1;
                    let data = date.getDate();
                    let hours = date.getHours();
                    let minutes = date.getMinutes();
                    let seconds = date.getSeconds();
                    let item = {text:this.newItem, data:year + '.' + addZero(month) + '.' + addZero(data) + ' ' + addZero(hours) + ':' + addZero(minutes) + ':' + addZero(seconds)};
                    this.items.push(item);
                    this.newItem = '';
                }
            }
        } 
}
</script>