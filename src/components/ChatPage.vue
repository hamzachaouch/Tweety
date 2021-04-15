<template>
  <q-page ref="pageChat" class="flex column">
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
              :bg-color="msg.from === 'me' ? 'amber-7' : 'info'"
              :text-color="msg.from === 'me' ? '' : 'white'"
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
