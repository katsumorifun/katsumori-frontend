<template>
  <div class="filter-container">
    <div class="d-lg-block" v-bind:class="{'d-none': closeFilter}">
      <div class="col-12">
        <div class="filter-block">
          <div class="body">
            <div class="row">
              <div class="col-auto me-auto">
                <h6 class="p-title">{{$tc('filter', 2)}}</h6>
              </div>
              <div class="col-auto">
                <div class="button" v-on:click="filterOnClick"> {{$t('apply')}} </div>
              </div>
            </div>
          </div>
          <div class="filter">
            <div class="selector-block">
              <div class="selector">
                <div class="placeholder">
                  <div class="selected">
                    <span>{{$t('animes.anime.status')}}</span>
                  </div>
                </div>
                <div class="chek-box-list">
                  <ul>
                    <li v-for="statusItem in status" :key="statusItem.status_id" :title="statusItem.nameRu" v-bind:class="{selected: statusItem.selected }">
                      <label>
                        <input type="checkbox" v-model="statusItem.selected"><span>{{statusItem['name_' + getLocale]}}</span>
                      </label>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="selector-block">
              <div class="selector">
                <div class="placeholder">
                  <div class="selected">
                    <span>{{$t('animes.anime.type')}}</span>
                  </div>
                </div>
                <div class="chek-box-list">
                  <ul>
                    <li v-for="type in types" :key="type.id" :title="type.nameEn" v-bind:class="{selected: type.selected }">
                      <label><input type="checkbox" v-model="type.selected"><span>{{type['name_' + getLocale]}}</span></label>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="selector-block">
              <div class="selector">
                <div class="placeholder">
                  <div class="selected">
                    <span>{{$t('animes.anime.genres')}}</span>
                  </div>
                </div>
                <div class="chek-box-list">
                  <ul>
                    <li data-value="#" v-for="genre in genres" :key="genre.genre_id" :title="genre.title" v-bind:class="{selected: genre.selected }">
                      <label><input type="checkbox" v-model="genre.selected"><span>{{genre['name_' + getLocale]}}</span></label>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="selector-block">
              <div class="selector">
                <div class="placeholder">
                  <div class="selected">
                    <span>{{$t('animes.anime.rating')}}</span>
                  </div>
                </div>
                <div class="chek-box-list">
                  <ul>
                    <li v-for="rating in ratings" :key="rating.rating_id" :title="rating['title_' + getLocale]" v-bind:class="{selected: rating.selected }">
                      <label><input type="checkbox" v-model="rating.selected"><span>{{rating.name}}</span></label>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="selector-block">
              <div class="selector">
                <div class="placeholder">
                  <div class="selected">
                    <span>{{$t('episode duration')}}</span>
                  </div>
                </div>
                <div class="chek-box-list">
                  <ul>
                    <li v-for="duration in durations" :key="duration.duration_id" :title="duration.title" v-bind:class="{selected: duration.selected }">
                      <label>
                        <input type="checkbox" v-model="duration.selected"><span>{{duration['name_' + getLocale]}}</span>
                      </label>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="selector-block">
              <div class="selector">
                <div class="placeholder">
                  <div class="selected">
                    <span>{{$t('animes.anime.season')}}</span>
                  </div>
                </div>
                <div class="chek-box-list">
                  <ul>
                    <li v-for="season in seasons" :key="season.season_id" :title="season.nameRu" v-bind:class="{selected: season.selected }">
                      <label>
                        <input type="checkbox" v-model="season.selected"><span>{{season['name_' + getLocale]}}</span>
                      </label>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="selector-block">
              <div class="selector">
                <div class="placeholder">
                  <div class="selected">
                    <span>{{$t('animes.anime.score')}}</span>
                  </div>
                </div>
                <div class="chek-box-list">
                  <ul>
                    <li data-field="status" data-value="anons">
                      <input autocomplete="off" type="checkbox"><span>8+</span>
                    </li>
                    <li data-field="status" data-value="anons">
                      <input autocomplete="off" type="checkbox"><span>7+</span>
                    </li>
                    <li data-field="status" data-value="anons">
                      <input autocomplete="off" type="checkbox"><span>6+</span>
                    </li>
                    <li data-field="status" data-value="anons">
                      <input autocomplete="off" type="checkbox"><span>5+</span>
                    </li>
                    <li data-field="status" data-value="anons">
                      <input autocomplete="off" type="checkbox"><span><5</span>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="selector-block">
              <div class="selector">
                <div class="placeholder">
                  <div class="selected">
                    <span>{{$t('my list')}}</span>
                  </div>
                </div>
                <div class="chek-box-list">
                  <ul>
                    <li data-field="status">
                      <input autocomplete="off" type="checkbox"><span>{{$t('completed')}}</span>
                    </li>
                    <li data-field="status">
                      <input autocomplete="off" type="checkbox"><span>{{$t('plan to watch')}}</span>
                    </li>
                    <li data-field="status">
                      <input autocomplete="off" type="checkbox"><span>{{$t('dropped')}}</span>
                    </li>
                    <li data-field="status">
                      <input autocomplete="off" type="checkbox"><span>{{$t('on-hold')}}</span>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
            <div class="selector-block pb-5">
              <div class="selector sort cursor-drop" v-on:click="openSort">
                <div class="placeholder">
                  <div class="selected">
                    <span>{{$t('sorted by')}}</span>
                  </div>
                  <div class="icon-inline dropdown-icon">
                    <svg xmlns="http://www.w3.org/2000/svg" width="10" height="6" viewBox="0 0 10 6">
                      <path fill="#FFF" fill-rule="nonzero" d="M8.618 5.772l.003.003c.35.336.873.29 1.174-.102a1.04 1.04 0 0 0-.078-1.334L5.55.233a.765.765 0 0 0-1.1 0L.28 4.342c-.342.345-.375.94-.075 1.331.301.393.825.438 1.177.099L5 2.207l3.618 3.565z"></path>
                    </svg>
                  </div>
                </div>
                <div class="drop-options">
                  <div class="item">
                    ???? ????????????????
                  </div>
                  <div class="item">
                    ???? ????????????????
                  </div>
                  <div class="item">
                    ???? ???????? ????????????????
                  </div>
                  <div class="item">
                    ???? ???????? ????????????
                  </div>
                </div>
              </div>
            </div>
          </div>
          <div class="footer">
            <div class="d-grid gap-2 button-block mx-0">
              <div class="btn" type="button">{{$t('reset filter')}}</div>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="btn-filter d-block d-lg-none" v-on:click="filterOnClick()">
      <i class="bi bi-filter-circle-fill"></i>
    </div>
  </div>

</template>

<script>

import {mapGetters} from "vuex";

export default {
  name: "AnimeFilterComponent",
  computed: mapGetters(['getLocale']),
  data: function (){
    return {
      closeFilter: true,

      status: [
        {
          "status_id": 1,
          "selected":  false,
          "name_jp":    "",
          "name_en":    "Announced",
          "name_ru":    "????????????????????????"
        },
        {
          "status_id": 2,
          "selected":  false,
          "name_jp":    "",
          "name_en":    "Ongoing",
          "name_ru":    "??????????????"
        },
        {
          "status_id": 3,
          "selected":  false,
          "name_jp":    "",
          "name_en":    "Released",
          "name_ru":    "??????????"
        },
      ],
      types:  [
        {
          "type_id": 1,
          "selected":  false,
          "name_jp":    "",
          "name_en":    "Tv serial",
          "name_ru":    "Tv ????????????"
        },
        {
          "type_id":   2,
          "selected":  false,
          "name_jp":    "",
          "name_en":    "Film",
          "name_ru":    "??????????"
        },
        {
          "type_id":   3,
          "selected":  false,
          "name_jp":    "",
          "name_en":    "OVA",
          "name_ru":    "OVA"
        },
        {
          "type_id":   4,
          "selected":  false,
          "name_jp":    "",
          "name_en":    "ONA",
          "name_ru":    "ONA"
        },
        {
          "type_id":   5,
          "selected":  false,
          "name_jp":    "",
          "name_en":    "Special",
          "name_ru":    "??????????"
        },
        {
          "type_id":   6,
          "selected":  false,
          "name_jp":    "",
          "name_en":    "Clip",
          "name_ru":    "????????"
        },
      ],
      genres: [
        {
          "genre_id": 1,
          "selected": false,
          "name_jp":  "??????",
          "name_en":  "Shounen",
          "name_ru":  "??????????",
          "title":   "??????????, ?????????? ?? ????????????, ???????????????????????? ???? ???????????? ?????????????? ?????????????????? ??? ?????????????????? ?? ???????????? ?? ???????????????? ???? 12 ???? 18 ??????. ?????????? ?????????? ???????? ?????????????????????? ?? ???????????????????????????????????? ???????????????? (?????????????????? ???????????????????? ???????? ????????????????), ???????????????????? 38,4% ??????????"
        },
        {
          "genre_id": 2,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Shounen Ai",
          "name_ru": "??????????-????",
          "title":  "?????????????????????????? ?????????? ?? ??????????, ?????????????? ??????????, ?????????????????????? ???????????????????????????????? ?????????? ?????????? ?????????????? ?????? ??????????????????, ?????? ???????????????? ?????????????? ???????????????????? ???????????????? ??????????????. ???????????????????????? ???? ?????????????????????????? ????????????????????, ?? ???? ??????????????????????.",
        },
        {
          "genre_id": 3,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Seinen",
          "name_ru": "????????????",
          "title":  "?????????? ?? ??????????, ???????????????????????? ???? ???????????? ?????????????? ?????????????????? ??? ?????????????? ???????????? ???? 18 ?????? ?? ????????????. ?????????? ?????????? ???????? ?????????????????????? ?? ???????????????????????????????????? ????????????-???????????????? (?????????????????? ???????????????????? ???????? ????????????????). ?? ???????????? ?????????????? ???????????????????????? ?? ?????????? ???????????? ???????????????? ???? ?????????????????? ?????????????????????? ?? ???????????????? ???? 40 ??????."
        },
        {
          "genre_id": 4,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Shoujo",
          "name_ru": "??????????",
          "title":  "",
        },
        {
          "genre_id": 5,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Shoujo Ai",
          "name_ru": "??????????-????",
          "title":  "",
        },
        {
          "genre_id": 6,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Josei",
          "name_ru": "????????????",
          "title":  "",
        },
        {
          "genre_id": 7,
          "selected": false,
          "name_jp": "???????????????????????????",
          "name_en": "Gender Bender",
          "name_ru": "?????????? ????????",
          "title":  "",
        },
        {
          "genre_id": 8,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Comedy",
          "name_ru": "??????????????",
          "title":  "",
        },
        {
          "genre_id": 9,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Romance",
          "name_ru": "??????????????????",
          "title":  "",
        },
        {
          "genre_id": 10,
          "selected": false,
          "name_jp": "??????",
          "name_en": "School",
          "name_ru": "??????????",
          "title":  "",
        },
        {
          "genre_id": 11,
          "selected": false,
          "name_jp": "???????????????",
          "name_en": "Action",
          "name_ru": "??????????",
          "title":  "",
        },
        {
          "genre_id": 12,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Adventure",
          "name_ru": "??????????????????????",
          "title":  "",
        },
        {
          "genre_id": 13,
          "selected": false,
          "name_jp": "???",
          "name_en": "Cars",
          "name_ru": "????????????",
          "title":  "",
        },
        {
          "genre_id": 14,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Dementia",
          "name_ru": "??????????????",
          "title":  "",
        },
        {
          "genre_id": 15,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Demons",
          "name_ru": "????????????",
          "title":  "",
        },
        {
          "genre_id": 16,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Drama",
          "name_ru": "??????????",
          "title":  "",
        },
        {
          "genre_id": 17,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Ecchi",
          "name_ru": "????????",
          "title":  "",
        },
        {
          "genre_id": 18,
          "selected": false,
          "name_jp": "???????????????",
          "name_en": "Fantasy",
          "name_ru": "????????????????????",
          "title":  "",
        },
        {
          "genre_id": 19,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Game",
          "name_ru": "????????",
          "title":  "",
        },
        {
          "genre_id": 20,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Harem",
          "name_ru": "??????????",
          "title":  "",
        },
        {
          "genre_id": 21,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Historical",
          "name_ru": "????????????????????????",
          "title":  "",
        },
        {
          "genre_id": 22,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Horror",
          "name_ru": "??????????",
          "title":  "",
        },
        {
          "genre_id": 23,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Kids",
          "name_ru": "??????????????",
          "title":  "",
        },
        {
          "genre_id": 24,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Magic",
          "name_ru": "??????????",
          "title":  "",
        },
        {
          "genre_id": 25,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Martial Arts",
          "name_ru": "???????????? ??????????????????",
          "title":  "",
        },
        {
          "genre_id": 26,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Mecha",
          "name_ru": "????????",
          "title":  "",
        },
        {
          "genre_id": 27,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Military",
          "name_ru": "??????????????",
          "title":  "",
        },
        {
          "genre_id": 28,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Music",
          "name_ru": "????????????",
          "title":  "",
        },
        {
          "genre_id": 29,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Mystery",
          "name_ru": "????????????????",
          "title":  "",
        },
        {
          "genre_id": 30,
          "selected": false,
          "name_jp": "???????????????",
          "name_en": "Parody",
          "name_ru": "??????????????",
          "title":  "",
        },
        {
          "genre_id": 31,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Police",
          "name_ru": "??????????????",
          "title":  "",
        },
        {
          "genre_id": 32,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Psychological",
          "name_ru": "??????????????????????????????",
          "title":  "",
        },
        {
          "genre_id": 33,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Samurai",
          "name_ru": "??????????????",
          "title":  "",
        },
        {
          "genre_id": 34,
          "selected": false,
          "name_jp": "???????????????",
          "name_en": "Sci-Fi",
          "name_ru": "????????????????????",
          "title":  "",
        },
        {
          "genre_id": 35,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Slice of Life",
          "name_ru": "????????????????????????????",
          "title":  "",
        },
        {
          "genre_id": 36,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Space",
          "name_ru": "????????????",
          "title":  "",
        },
        {
          "genre_id": 37,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Sports",
          "name_ru": "??????????",
          "title":  "",
        },
        {
          "genre_id": 38,
          "selected": false,
          "name_jp": "?????????????????????",
          "name_en": "Super Power",
          "name_ru": "?????????? ????????",
          "title":  "",
        },
        {
          "genre_id": 39,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Supernatural",
          "name_ru": "????????????????????????????????????",
          "title":  "",
        },
        {
          "genre_id": 40,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Vampire",
          "name_ru": "??????????????",
          "title":  "",
        },
        {
          "genre_id": 41,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Thriller",
          "name_ru": "??????????????",
          "title":  "",
        },
        {
          "genre_id": 42,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Hentai",
          "name_ru": "????????????",
          "title":  "",
        },
        {
          "genre_id": 43,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Yaoi",
          "name_ru": "??????",
          "title":  "",
        },
        {
          "genre_id": 44,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Yuri",
          "name_ru": "??????",
          "title":  "",
        },
        {
          "genre_id": 45,
          "selected": false,
          "name_jp": "???????????????",
          "name_en": "Shotacon",
          "name_ru": "??????????????",
          "title":  "",
        },
        {
          "genre_id": 46,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Tokusatsu",
          "name_ru": "????????????????",
          "title":  "",
        },
        {
          "genre_id": 47,
          "selected": false,
          "name_jp": "????????????????????????",
          "name_en": "Post apocalyptic",
          "name_ru": "???????? ??????????????????????",
          "title":  "",
        },
        {
          "genre_id": 48,
          "selected": false,
          "name_jp": "?????????????????????",
          "name_en": "Steampunk",
          "name_ru": "????????????????",
          "title":  "",
        },
        {
          "genre_id": 49,
          "selected": false,
          "name_jp": "?????????",
          "name_en": "Otaku",
          "name_ru": "????????????",
          "title":  "",
        },
        {
          "genre_id": 50,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Makho-shodze",
          "name_ru": "????????-??????????",
          "title":  "",
        },
        {
          "genre_id": 51,
          "selected": false,
          "name_jp": "?????????????????????",
          "name_en": "Cyberpunk",
          "name_ru": "??????????????????",
          "title":  "",
        },
        {
          "genre_id": 52,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "Phantom thieves",
          "name_ru": "??????????",
          "title":  "",
        },
        {
          "genre_id": 53,
          "selected": false,
          "name_jp": "??????",
          "name_en": "Ikuji",
          "name_ru": "????????????",
          "title":  "",
        },
        {
          "genre_id": 54,
          "selected": false,
          "name_jp": "????????????",
          "name_en": "idol",
          "name_ru": "????????????",
          "title":  "",
        },
        {
          "genre_id": 55,
          "selected": false,
          "name_jp": "?????? ",
          "name_en": "Josei",
          "name_ru": "????????????",
          "title":  "",
        }
      ],
      ratings: [
        {
          "rating_id":    1,
          "selected":     false,
          "name":         "G",
          "title_jp":     "??????????????????",
          "title_en":     "No age restrictions",
          "title_ru":     "?????? ???????????????????? ??????????????????????",
        },
        {
          "rating_id":    2,
          "selected":     false,
          "name":         "PG",
          "title_jp":     "??????????????????????????????????????????????????????????????????????????????",
          "title_en":     "There is no age limit, but the presence of parents is recommended",
          "title_ru":     "?????? ???????????????????? ??????????????????????, ???? ?????????????????????????? ?????????????????????? ??????????????????",
        },
        {
          "rating_id":    3,
          "selected":     false,
          "name":         "PG-13",
          "title_jp":     "13 ????????????????????????????????????????????????????????????",
          "title_en":     "Viewing is not desirable for children under 13",
          "title_ru":     "?????????? ???? 13 ?????? ???????????????? ???? ??????????????????",
        },
        {
          "rating_id":   5,
          "selected":    false,
          "name":        "R-17",
          "title_jp":     "17 ??????????????????????????????????????????????????????",
          "title_en":     "Persons under the age of 17 are allowed to watch only with their parents",
          "title_ru":     "?????????? ???? ?????????????????? 17 ?????????? ???????????????? ???????????????? ???????????? ?? ????????????????????",
        },
        {
          "rating_id":    6,
          "selected":     false,
          "name":         "R+",
          "title_jp":     "17 ???????????????????????????????????????????????????",
          "title_en":     "Persons under the age of 17 are prohibited from viewing",
          "title_ru":     "?????????? ???? ?????????????????? 17 ?????????? ???????????????? ????????????????",
        },
        {
          "rating_id":   7,
          "selected":    false,
          "name":        "RX",
          "title_jp":     "",
          "title_en":     "18+ content",
          "title_ru":     "18+ ??????????????",
        },
      ],
      durations: [
        {
          "duration_id": 1,
          "selected": false,
          "name_jp":  "??????6???",
          "name_en":  "Up to 6 minutes",
          "name_ru":  "???? 6 ??????????",
        },
        {
          "duration_id": 2,
          "selected": false,
          "name_jp":  "??????14???",
          "name_en":  "Up to 14 minutes",
          "name_ru":  "???? 14 ??????????",
        },
        {
          "duration_id": 3,
          "selected": false,
          "name_jp":  "??????30???",
          "name_en":  "Up to 30 minutes",
          "name_ru":  "???? 30 ??????????",
        },
        {
          "duration_id": 4,
          "selected": false,
          "name_jp":  "30?????????\n",
          "name_en":  "More than 30 minutes",
          "name_ru":  "?????????? 30 ??????????",
        },
      ],
      seasons:   [
        {
          "season_id": 1,
          "selected": false,
          "name_jp":  "???",
          "name_en":  "Winter",
          "name_ru":  "????????",
        },
        {
          "season_id": 2,
          "selected": false,
          "name_jp":  "??????",
          "name_en":  "Spring",
          "name_ru":  "??????????",
        },
        {
          "season_id": 3,
          "selected": false,
          "name_jp":  "???",
          "name_en":  "Summer",
          "name_ru":  "????????",
        },
        {
          "season_id": 4,
          "selected": false,
          "name_jp":  "???",
          "name_en":  "Autumn",
          "name_ru":  "??????????",
        },
      ],
      selectedStatus:    "",
      selectedGenres:    "",
      selectedTypes:     "",
      selectedRatings:   "",
      selectedDurations: "",
    }
  },
  watch: {
    genres: {
      handler(){
        this.selectedGenres = "";
        this.genres.forEach((genreItem) => {
          if(genreItem.selected){
            this.selectedGenres += genreItem.nameEn + ",";
          }
        })
        this.selectedGenres = this.selectedGenres.slice(0, -1);
        this.updateFiler();
      },
      deep: true
    },
    status: {
      handler(){
        this.selectedStatus = "";
        this.status.forEach((statusItem) => {
          if(statusItem.selected){
            this.selectedStatus += statusItem.name_en + ",";
          }
        })
        this.selectedStatus = this.selectedStatus.slice(0, -1);
        this.updateFiler();
      },
      deep: true
    },
    types: {
      handler(){
        this.selectedTypes = "";
        this.types.forEach((typesItem) => {
          if(typesItem.selected){
            this.selectedTypes += typesItem.name_en + ",";
          }
        })
        this.selectedTypes = this.selectedTypes.slice(0, -1);
        this.updateFiler();
      },
      deep: true
    },
    ratings: {
      handler(){
        this.selectedRatings = "";
        this.ratings.forEach((ratingsItem) => {
          if(ratingsItem.selected){
            this.selectedRatings += ratingsItem.name + ",";
          }
        })
        this.selectedRatings = this.selectedRatings.slice(0, -1);
        this.updateFiler();
      },
      deep: true
    },
    durations: {
      handler(){
        this.selectedDurations = "";
        this.durations.forEach((durationItem) => {
          if(durationItem.selected){
            this.selectedDurations += durationItem.name_en + ",";
          }
        })
        this.selectedDurations = this.selectedDurations.slice(0, -1);
        this.updateFiler();
      },
      deep: true
    },
    seasons: {
      handler(){
        this.updateFiler();
      },
      deep: true
    },
  },

  methods: {
    filterOnClick(){
      this.closeFilter = !this.closeFilter;
    },
    updateFiler(){
      this.$router.replace({
        query:{
          status: this.selectedStatus,
          ratings: this.selectedRatings,
          types: this.selectedTypes,
          genres: this.selectedGenres,
          durations: this.selectedDurations
        }
      }).catch(e => {});
    },
    openSort(){
      let selectorSort = document.getElementsByClassName('selector sort')[0];
      if(!selectorSort.classList.contains('open')){
        selectorSort.classList.add('open');
      }
      else{
        selectorSort.classList.remove('open');
      }
    }
  },
}
</script>

<style scoped>
  .filter{
    color: var(--text-color);
    padding: 0;
  }
  .filter > .selector-block{
    box-sizing: border-box;
    margin-bottom: 20px;
  }
  .selector > .chek-box-list > ul > li.selected {
    background: #3490dc;
    border-radius: 0.4rem;
  }
  .selector-block > .selector > .placeholder{
    cursor: inherit;
    box-sizing: border-box;
    padding: 10px 15px;
    font-size: 14px;
    font-weight: bolder;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.43;
    letter-spacing: normal;
    justify-content: space-between;
    display: flex;
    align-items: center;
  }
  .selector-block > .selector.cursor-drop > .placeholder{
    cursor: pointer;
  }
  .selector-block > .selector > .placeholder >.selected{
    font-size: 16px;
    font-weight: 800;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.43;
    letter-spacing: normal;
    box-sizing: border-box;
    display: flex;
    -webkit-box-align: center;
    align-items: center;
  }
  .selector-block > .selector > .placeholder >.icon-inline.dropdown-icon{
    font-size: 14px;
    font-weight: 400;
    font-stretch: normal;
    font-style: normal;
    line-height: 1.43;
    letter-spacing: normal;
    box-sizing: border-box;
    -webkit-box-flex: 0;
    flex: 0 0 6px;
    margin-right: 6.5px;
    transition: transform .2s,-webkit-transform .2s;
    transform: rotate(270deg);
  }
  .selector-block > .selector.open > .placeholder >.icon-inline.dropdown-icon{
    transform: rotate(179deg);
  }
  .selector-block > .selector > .placeholder >.icon-inline.dropdown-icon > svg{
    color: black;
  }
  .selector-block > .selector > .drop-options{
    display: none;
    font-size: 14px;
    box-sizing: border-box;
    left: 0;
    position: inherit;
    width: 100%;
    z-index: 20;
    overflow-y: auto;
    max-height: 200px;
    border-radius: 0 0 14px 14px;
    transform: scale(1);
  }
  .selector-block > .selector.open > .drop-options{
    display: block;
  }
  .selector-block > .selector > .drop-options > .item{
    font-size: 14px;
    box-sizing: border-box;
    user-select: none;
    border-bottom: 1px solid rgba(61,64,74,.4);
    padding: 12px 15px;
}
.selector-block .selector .chek-box-list ul li{
  -moz-user-select: none;
  user-select: none;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  font-size: 12px;
  line-height: 20.34px;
  padding: 1px 3px 0;
  margin: 1px 0 0.5rem;
}
.selector-block .selector .chek-box-list ul li label{
  font-size: .8rem;
  padding-bottom: 0.3rem;
  padding-top: 0.3rem;
}
.selector-block .selector .chek-box-list ul li label > input {
  display: none;
}
.selector-block .selector .chek-box-list ul{
  margin-left: 2px;
  padding-left: 2px;
}
.filter-block > .body{
  background: #009BEB;
  height: 7vh;
  display: none;
}
.filter-block > .body{
  padding-left: 1rem;
  padding-right: 1rem;
  padding-top: 2.2vh;
}
.filter-block > .body > .row > .col-auto > .button{
  height: 100%;
  background: #dfdfe0;
  border-radius: 7px;
  padding: 0.2rem;
}
@media (min-width: 991px) {
  .selector-block .selector .chek-box-list ul li label > span{
    margin-left: 17px;
  }
}
/* Small devices (landscape phones, 991px and up) */
@media (max-width: 991px) {
  .filter-block .filter {
    border-radius: 0;
    height: 100%;
    padding-bottom: 2rem;
    overflow: auto;
    background: #0f1318;
  }
  .selector-block > .selector > .placeholder{
    background: none;
  }
  .filter-block > .body{
    display: block;
  }
  .filter-block > .footer{
    position: absolute;
    bottom: 0;
    width: 100%;
  }
  .filter-block > .footer .btn{
    background: #009beb;
    border-radius: 0;
  }
  .selector-block .selector .chek-box-list{
    overflow-x: auto;
    overflow-y: hidden;
  }
  .selector-block .selector .chek-box-list ul li{
    font-size: 17px;
    white-space: pre;
    overflow: inherit;
    display: inline;
    padding: 8px 12px 8px;
    margin: 0 4px;
    text-align:center;
  }
  .selector > .chek-box-list > ul > li > label > input {
    display: none;
  }
  .selector > .chek-box-list > ul{
    display:flex;
    list-style:none;
  }
  .filter-block{
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    z-index: 1000;
  }
}
.btn-filter{
  position: fixed;
  width: 7rem;
  bottom: 3.5rem;
  right: -0.2rem;
  z-index: 4;
  filter: drop-shadow(2px 3px 8px rgba(0, 0, 0, 2.25));
}
.btn-filter > i{
  font-size: 4.5rem;
  color: var(--text-color);
}
</style>