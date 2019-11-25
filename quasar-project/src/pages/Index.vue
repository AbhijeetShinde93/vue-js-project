<template>
  <q-page class="flex flex-center">
    <div class="q-pa-md">
      <div class="row">
        <div class="col-8">
          <h4>Search Tool for direct download file links</h4>
          <q-input v-model="text" label="Type Here To Search" />
          <div class="q-gutter-sm">
            <q-checkbox v-model="teal" label="All" />
          </div>
        </div>

        <div class="col-4">
          <h4>What is File Hunter?</h4>
          <p>
            File Hunter is an advanced file search tool. File Hunter searches
            links on internet which can be directly downloaded without torrent.
          </p>
          <h4>How to use File Hunter?</h4>
          <p>
            Using file hunter is straight forward. All you have to do is enter
            your search criteria into text box and select category you want to
            search for. For example if you want to search for funny videos,
            enter funny in text box and tick the videos checkbox, this will
            limit your search results to video files names matching to funny.
            After you tick correct checkbox, you have to click on search icon
            next to text box, this will open search results in new tab
            containing multiple links. Click on any link and it will show list
            of all files available to download. Now all you have to do is click
            on filename you want to download, it will immediately start
            downloading.
          </p>
        </div>
      </div>
    </div>
  </q-page>
</template>

<script>
export default {
  name: "PageIndex",
  data() {
    return {
      teal: true,
      orange: false,
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
            { name: ".mobi", status: false },
            { name: ".cbz", status: false },
            { name: ".cbr", status: false }
          ],
          addons: []
        }
      ]
    };
  }
};
</script>
