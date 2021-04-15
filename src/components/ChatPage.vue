<template>
  <q-page ref="pageChat" class="flex column page-chat">
    <div class="q-pa-md row  column col justify-end">
      <template class="full-width">
        <div class="q-pa-md row justify-center ">
          <div style="width: 100%; max-width: 400px">
            <q-chat-message
              :key="msg.text"
              v-for="msg in messages"
              :name="msg.from"
              :avatar="
                msg.from === 'me'
                  ? 'https://cdn.quasar.dev/img/avatar1.jpg'
                  : 'https://cdn.quasar.dev/img/avatar5.jpg'
              "
              :text="[msg.text]"
              stamp="7 minutes ago"
              :sent="msg.from === 'me' ? true : false"
              :bg-color="msg.from === 'me' ? 'grey-8' : 'info'"
              text-color="white"
            />
          </div>
        </div>
      </template>
      <q-footer class="flex column" bordered>
        <q-toolbar class="q-mt-md">
          <q-input
            color="info"
            label-color="grey-5"
            autogrow
            @keyup.enter="sendMsg"
            bottom-slots
            outlined
            rounded
            class="full-width"
            v-model="newMsg"
            label="Send a Message..."
            dense
          >
            <template v-slot:after>
              <q-btn @click="sendMsg" round dense flat icon="send" />
            </template>
          </q-input>
        </q-toolbar>
      </q-footer>
    </div>
  </q-page>
</template>

<script>
export default {
  name: "ChatPage",
  data() {
    return {
      newMsg: "",
      messages: [
        {
          id: 1,
          text: "Hello ,how are you ?",
          from: "me"
        },
        {
          id: 2,
          text: "i 'm fine thanks, and you?",
          from: "Soumaya"
        }
      ]
    };
  },
  watch: {
    messages: function(val) {
      if (Object.keys(val).length) {
        this.scrollToButtom();
      }
    }
  },
  methods: {
    scrollToButtom() {
      let pageChat = this.$refs.pageChat.$el;
      setTimeout(() => {
        window.scrollTo(0, pageChat.scrollHeight);
      }, 20);
    },
    sendMsg() {
      let msgwritten = {};
      msgwritten.text = this.newMsg;
      msgwritten.from = "me";
      this.messages.push(msgwritten);
      this.newMsg = "";
    }
  }
};
</script>
<style lang="stylus">
.page-chat
    background #dddddd
    &:after
        content ''
        display block
        position fixed
        left 0
        top 0
        right 0
        bottom 0
        z-index 0
        opacity 0.1
        background-color:silver;background-image:radial-gradient(circle at 100% 150%, silver 24%, white 24%, white 28%, silver 28%, silver 36%, white 36%, white 40%, transparent 40%, transparent),radial-gradient(circle at 0    150%, silver 24%, white 24%, white 28%, silver 28%, silver 36%, white 36%, white 40%, transparent 40%, transparent),radial-gradient(circle at 50%  100%, white 10%, silver 10%, silver 23%, white 23%, white 30%, silver 30%, silver 43%, white 43%, white 50%, silver 50%, silver 63%, white 63%, white 71%, transparent 71%, transparent),radial-gradient(circle at 100% 50%, white 5%, silver 5%, silver 15%, white 15%, white 20%, silver 20%, silver 29%, white 29%, white 34%, silver 34%, silver 44%, white 44%, white 49%, transparent 49%, transparent),radial-gradient(circle at 0    50%, white 5%, silver 5%, silver 15%, white 15%, white 20%, silver 20%, silver 29%, white 29%, white 34%, silver 34%, silver 44%, white 44%, white 49%, transparent 49%, transparent);background-size: 100px 50px;
q-chat-message
    z-index 2
</style>
