<template>
  <q-page padding>
    <div class="row">
      <div class="col-8" style="padding-right:25px">
        <h5 style="margin:0;">Search Tool for direct download file links</h5>
        <q-input v-model="search" placeholder="Type Here To Search" style="padding-bottom:5px"/>

        <q-checkbox
          v-model="allStatus"
          label="All"
          @click.native="disableAllFilters()"
        />

        <div v-for="filter in filters" :key="filter.name">
          <q-checkbox
            v-model="filter.status"
            :label="filter.name"
            :value="filter.name"
            @click.native="disableAll()"
          />

          <div v-if="filter.status">
            <q-checkbox
              style="margin-left:20px"
              v-for="extension in filter.extensions"
              :key="extension.name"
              v-model="extension.status"
              :label="extension.name"
              :value="extension.name"
            />
          </div>

          <div v-if="filter.status">
            <q-checkbox
              style="margin-left:20px"
              v-for="addon in filter.addons"
              :key="addon.name"
              v-model="addon.status"
              :label="addon.name"
              :value="addon.name"
            ></q-checkbox>
          </div>
        </div>

        <!---custom checbox---->
        <div v-if="customExtensions.length">
          <div class="q-gutter-sm">
            <q-checkbox
              v-model="checkCustom"
              label="Custom"
              @click.native="uncheckAll()"
            />
          </div>
          <div v-if="checkCustom" style="margin-left:20px">
            <q-checkbox
              v-for="custom in customExtensions"
              :key="custom.name"
              v-model="custom.status"
              :label="custom.name"
              :value="custom.name"
            />
          </div>
        </div>

        <!---input textbox---->
        <div class="row" style="padding-bottom:10px">
          <q-input
            outlined
            v-model="customText"
            label="Add Custom Extension"
            class="col-4"
          >
            <template v-slot:append>
              <q-icon name="add" v-on:click="addCustom()" /> </template
          ></q-input>
        </div>
      </div>

      <div class="col-4">
        <h5 style="margin:0">What is File Hunter?</h5>
        <p>
          File Hunter is an advanced file search tool. File Hunter searches
          links on internet which can be directly downloaded without torrent.
        </p>
        <h5 style="margin:1">How to use File Hunter?</h5>
        <p>
          Using file hunter is straight forward. All you have to do is enter
          your search criteria into text box and select category you want to
          search for. For example if you want to search for funny videos, enter
          funny in text box and tick the videos checkbox, this will limit your
          search results to video files names matching to funny. After you tick
          correct checkbox, you have to click on search icon next to text box,
          this will open search results in new tab containing multiple links.
          Click on any link and it will show list of all files available to
          download. Now all you have to do is click on filename you want to
          download, it will immediately start downloading.
        </p>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      allStatus: true,
      checkCustom: true,
      search: "",
      customExtensions: [],
      customText: "",
      filters: [
        {
          name: "Movies / TV Shows / Videos",
          status: false,
          extensions: [
            { name: ".mkv", status: true },
            { name: ".mpv4", status: true },
            { name: ".avi", status: true }
          ],
          addons: [
            { name: "720p", status: false },
            { name: "1080p", status: false },
            { name: "2160p", status: false }
          ]
        },
        {
          name: "Music / Audios",
          status: false,
          extensions: [
            { name: ".mp3", status: true },
            { name: ".wav", status: true },
            { name: ".ac3", status: true }
          ],
          addons: [
            { name: "128kbps", status: false },
            { name: "256kbps", status: false },
            { name: "320kbps", status: false }
          ]
        },
        {
          name: "Images / Graphics",
          status: false,
          extensions: [
            { name: ".jpeg", status: true },
            { name: ".jpg", status: true },
            { name: ".png", status: true }
          ],
          addons: [
            { name: "1280x720", status: false },
            { name: "1920x720", status: false },
            { name: "4096x2160", status: false }
          ]
        },
        {
          name: "Softwares / Games / Apps",
          status: false,
          extensions: [
            { name: ".exe", status: true },
            { name: ".iso", status: true },
            { name: ".tar", status: true }
          ],
          addons: []
        },
        {
          name: "Books / Docs",
          status: false,
          extensions: [
            { name: ".mobi", status: true },
            { name: ".cbz", status: true },
            { name: ".cbr", status: true }
          ],
          addons: []
        }
      ]
    };
  },
  methods: {
    addCustom() {
      if (!this.customText) {
        alert("Please enter some Extension");
      } else {
        this.checkCustom = true;
        this.customExtensions.push({ name: this.customText, status: true });
        this.customText = "";
        this.allStatus = false;
      }
    },
    disableAllFilters() {
      if (this.allStatus) {
        this.filters.forEach(filter => {
          filter.status = false;
        });
        this.checkCustom = false;
      }
    },
    disableAll() {
      let filterStatus = false;
      this.filters.forEach(filter => {
        if (filter.status) {
          filterStatus = true;
        }
      });
      if (this.checkCustom && this.customExtensions.length) {
        filterStatus = true;
      }
      this.allStatus = !filterStatus;
    },
    uncheckAll() {
      if (this.checkCustom) {
        this.allStatus = false;
      } else {
        this.allStatus = true;
      }
    }
  }
};
</script>
