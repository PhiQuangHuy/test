<v-menu
  content-class="date-picker"
  ref="pickerMenu"
  v-model="pickerMenu"
  :return-value.sync="searchForm.apiCallStartDate"
  :close-on-content-click="false"
  offset-y
  max-width="290px"
  min-width="290px"
>
  <template v-slot:activator="{ on }">
    <v-text-field
      class="default text-field-date pr-0"
      v-model='dateRangeText'
      label="전송일시"
      placeholder="YYYY.MM.DD - YYYY.MM.DD"
      v-on="on"
      readonly
      clearable
      @click="clickPicker"
    >
    </v-text-field>
  </template>
  <div @click="clickPicker">
    <v-date-picker
      v-model="searchForm.apiCallStartDate"
      range
      no-title
      scrollable
      :event-color="
        date =>
          date == searchForm.apiCallStartDate[0]
            ? ['startDate']
            : date == searchForm.apiCallStartDate[1]
            ? ['endDate']
            : ''
      "
      :events="searchForm.apiCallStartDate"
      :date-format="date => new Date(date).toDateString()"
      :locale="$i18n.locale"
      :picker-date.sync="pickerDate"
      @click:date="dateClick"
    >
      <v-spacer></v-spacer>
      <v-btn text :ripple="false" color="pink" @click="pickerMenu = false">{{ $t('button.close')}}</v-btn>
      <v-btn text :ripple="false" color="pink" @click="$refs.pickerMenu.save(searchForm.apiCallStartDate)">{{ $t('button.confirm')}}</v-btn>
    </v-date-picker>
  </div>
</v-menu>

export default {
  data: function () {
    return {
      pickerMenu: false,
      pickerStartMenu: false,
      pickerEndMenu: false,
      pickerDate: null,
      pickerStartDate: null,
      pickerEndDate: null
    }
  },
  watch: {
    pickerStartDate () {
      this.fnPickerDate()
    },
    pickerEndDate () {
      this.fnPickerDate()
    },
    pickerDate () {
      this.fnPickerDate()
    },
    pickerStartMenu () {
      this.fnPickerDate()
    },
    pickerEndMenu () {
      this.fnPickerDate()
    },
    pickerMenu () {
      this.fnPickerDate()
    }
  },
  methods: {
    // datepicker
    fnPickerDate () {
      this.removeKoDay() // 최초 Open 시
      setTimeout(() => {
        this.removeKoDay() // 월 변경 시
      }, 50)
      // here you can check if month changed using newval and oldval
      setTimeout(() => {
        // const actived = document.getElementsByClassName('v-btn--active')
        const oldSelected = document.querySelectorAll('.selected')
        if (oldSelected.length > 0) {
          for (var i = 0; i < oldSelected.length; i++) {
            oldSelected[i].classList.remove('selected')
          }
        }
        const selected = document.querySelectorAll('.v-date-picker-table__events')
        if (selected.length > 0) {
          this.$nextTick(() => {
            for (var j = 0; j < selected.length; j++) {
              selected[j].parentElement.classList.add('selected')
            }
          })
        }
      }, 50)
    },
    dateClick (date) {
      const _selectedItem = event.srcElement.parentElement
      setTimeout(() => {
        _selectedItem.classList.add('selected')
      }, 50)
    },
    clickPicker (evt) {
      const elYear = document.querySelector('ul.v-date-picker-years')
      const isYear = elYear !== false
      const isPrevButton = evt.target.tagName === 'BUTTON' !== false
      if (isYear) {
        this.buttonShow = isPrevButton !== true
      } else {
        this.buttonShow = true
      }
      this.removeKoDay() // 최초 Open 시
      setTimeout(() => {
        this.removeKoDay() // 월 변경 시
      }, 50)
    },
    removeKoDay () {
      const regDay = new RegExp('일')
      const el = document.querySelectorAll('div.v-btn__content')
      for (var i = 0; i < el.length; i++) {
        el[i].innerHTML = el[i].innerHTML.replace(regDay, '')
      }
    }
  }
}

