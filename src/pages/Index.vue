<template>
  <q-page>
    <div class="row">
      <div class="col">
        <ul style="color:red">
          <li class="text-subtitle1" v-for="(music, index) in musicList" v-bind:key="index">
            {{index}}: {{music.name}} by {{music.singer}}
            <button
              @click="editMusic(music, index)"
            >Edit</button>
            <button @click="deleteMusic(index)">Delete</button>
          </li>
        </ul>
      </div>
    </div>

    <div class="row">
      <div class="col-12">
        <input type="text" name v-model="text" placeholder="Name" id />
      </div>
      <div class="col-12">
        <input type="text" name v-model="singer" placeholder="Artist" id />
      </div>
      <button
        @click="isEdit ? updateMusic() : addMusic()"
      >{{ isEdit ? "Update Music" : "Add Music"}}</button>

      <!-- <button v-if="isEdit" @click="updateMusic()">Update Music</button>
      <button v-else @click="addMusic()">Add Music</button>-->
      <button @click="clearText()">Cancel</button>
    </div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      musicList: [
        { name: "Manok na Pula", singer: "Vic Desucatan" },
        { name: "Just Another Woman In Love", singer: "Anne Murray" }
      ],
      text: "",
      singer: "",
      isEdit: false,
      index: null
    };
  },
  methods: {
    //This is how to declare old function / long way
    // addMusic: function () {
    // }
    addMusic() {
      this.musicList.push({
        name: this.text,
        singer: this.singer
      });
      this.clearText();
    },
    clearText() {
      this.isEdit = false;
      this.text = "";
      this.singer = "";
    },
    editMusic(music, index) {
      this.index = index;
      this.isEdit = true;
      this.text = music.name;
      this.singer = music.singer;
    },
    deleteMusic(index) {
      this.musicList.splice(index, 1);
      alert("Music has been deleted!");
      this.clearText();
    },
    updateMusic() {
      this.$set(this.musicList, this.index, {
        name: this.text,
        singer: this.singer
      });
    }
  }
};
</script>
