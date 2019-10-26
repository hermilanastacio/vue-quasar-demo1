<template>
  <q-page class="q-ma-xl">
    <div class="row">
      <div class="col">
        <q-list bordered class="bg-grey-6">
          <q-item clickable v-ripple v-for="(music, index) in musicList" :key="index">
            <q-item-section>{{music.singer}}</q-item-section>
            <q-item-section>{{music.name}}</q-item-section>
            <q-item-section avatar>
              <q-btn round @click="editMusic(music, index)" color="primary" icon="edit" />
              <q-btn round @click="deleteMusic(index)" color="red" icon="delete" />
            </q-item-section>
          </q-item>
        </q-list>
        <!-- <ul style="color: red;">
          <li class="text-subtitle1" v-for="(music, index) in musicList" v-bind:key="index" >
            {{index}}: {{music.name}} by {{music.singer}}
            <button @click="editMusic(music, index)">Edit</button>
            <button @click="deleteMusic(index)">Delete</button>
          </li>
        </ul>-->
      </div>
    </div>
    <!-- <div class="row">
      <div class="col-12">
        <input type="text" name="" v-model="text" placeholder="Name" id="">
      </div>
      <div class="col-12">
        <input type="text" name="" v-model="singer" placeholder="Artist" id="">
      </div>
      <button @click="edit ? updateMusic() : addMusic()">{{edit ? "Update Music" : "Add Music"}}</button>
      2nd way
      <button v-if="edit" @click="updateMusic()">Update Music</button>
      <button v-else @click="addMusic()">Add Music</button>
      <button @click="clearText()">Cancel</button>
    </div>-->
    <q-dialog v-model="showForm" persistent transition-show="scale" transition-hide="scale">
      <q-card class="bg-teal text-white" style="width: 350px">
        <q-card-section>
          <div class="text-h6">{{edit ? "Update Music" : "Add Music"}}</div>
        </q-card-section>

        <q-card-section>
          <q-input standout="bg-teal text-white" v-model="text" label="Name of Music" />
          <q-input standout="bg-teal text-white" v-model="singer" label="Name of Artist" />
        </q-card-section>

        <q-card-actions align="right" class="bg-white text-teal">
          <q-btn
            flat
            :label="edit ? 'Update Music' : 'Add Music' "
            @click="edit ? updateMusic() : addMusic()"
          />
          <q-btn flat label="cancel" @click="clearText()" />
        </q-card-actions>
      </q-card>
    </q-dialog>
    <q-page-sticky position="bottom-right" :offset="[18, 18]">
      <q-btn fab icon="add" color="accent" @click="showForm = true" />
    </q-page-sticky>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      // comes from the database
      musicList: [
        { name: "Manok na Pula", singer: "Vic Desucatan" },
        { name: "Just Another Woman in Love", singer: "Anne Murray" }
      ],
      text: "",
      singer: "",
      edit: false,
      index: null,
      showForm: false
    };
  },
  methods: {
    addMusic() {
      this.musicList.push({
        name: this.text,
        singer: this.singer
      });
      this.clearText();
    },
    clearText() {
      this.edit = false;
      this.text = "";
      this.singer = "";
      this.showForm = false;
    },
    editMusic(music, index) {
      console.log(music);
      this.showForm = true;
      this.index = index;
      this.edit = true;
      this.text = music.name;
      this.singer = music.singer;
    },
    deleteMusic(index) {
      this.musicList.splice(index, 1);
      alert("Music data has been deleted!");
    },
    updateMusic() {
      //This updates the value of the object in array params={array, index, object to be replaced}
      this.$set(this.musicList, this.index, {
        name: this.text,
        singer: this.singer
      });
      this.clearText();
    }
  }
};
</script>