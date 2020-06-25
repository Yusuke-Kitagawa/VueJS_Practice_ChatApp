
<template>
  <div class="container chat">
    <h2 class="text-primary text-center">リアルタイムチャット</h2>
    <h5 class="text-secondary text-center">Vue.jsとFirebaseをかじってみました
    </h5>
    <div class="card total-item">
      <div class="card-body">
        <p class="text-secondary nomessage" v-if="messages.length == 0">
          [メッセージがありません！]
        </p>
        <div class="messages" v-chat-scroll="{always: false, smooth: true}">
          <div v-for="message in messages" :key="message.id">
            <span class="text-info">[{{message.name}}]:</span>
            <span>{{message.message}}</span>
            <span class="text-secondary time">{{message.timestamp}}</span>
          </div>
        </div>
      </div>
      <div class="card-action">
        <CreateMessage :name="name"/>
      </div>
    </div>
  </div>
</template>

<script>
import CreateMessage from '@/components/CreateMessage.vue';
import fb from '@/firebase/init.js';
import moment from 'moment';

export default {
  name: 'Chat',
  props:['name'],
  components:{
    CreateMessage
  },
  data(){
    return{
      messages:[]
    }
  },
  created(){
    let ref = fb.collection('messages').orderBy('timestamp');

    ref.onSnapshot(snapshot => {
      snapshot.docChanges().forEach(change => {
        if(change.type === 'added'){
          let doc = change.doc;
          this.messages.push({
            id: doc.id,
            name: doc.data().name,
            message: doc.data().message,
            timestamp: moment(doc.data().timestamp).format('LTS')
          });
        }
      });
    });
  }
}
</script>

<style>
.chat h2{
  font-size: 4.5vw;
  margin-bottom:  0;
}

.chat h5{
  font-size:2vw;
  margin-top:0;
  margin-bottom: 40px;
}

.chat span{
  font-size: 1.2em;
}

.chat .time{
  display:block;
  font-size: 0.7em;
}

.messages{
  max-height: 300px;
  overflow: auto;
}

.total-item{
  text-align:left;
}

</style>