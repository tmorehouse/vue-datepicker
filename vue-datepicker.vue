<style scoped>
.datepicker-overlay {
  position: fixed;
  width: 100%;
  height: 100%;
  z-index: 1050;
  top: 0;
  left: 0;
  overflow: hidden;
  -webkit-animation: fadein 0.5s;
  /* Safari, Chrome and Opera > 12.1 */
  -moz-animation: fadein 0.5s;
  /* Firefox < 16 */
  -ms-animation: fadein 0.5s;
  /* Internet Explorer */
  -o-animation: fadein 0.5s;
  /* Opera < 12.1 */
  animation: fadein 0.5s;
}
@keyframes fadein {
  from { opacity: 0; }
  to { opacity: 1; }
}
/* Firefox < 16 */
@-moz-keyframes fadein {
  from { opacity: 0; }
  to { opacity: 1;  }
}
/* Safari, Chrome and Opera > 12.1 */
@-webkit-keyframes fadein {
  from { opacity: 0; }
  to { opacity: 1; }
}
/* Internet Explorer */
@-ms-keyframes fadein {
  from { opacity: 0; }
  to { opacity: 1; }
}
/* Opera < 12.1 */
@-o-keyframes fadein {
  from { opacity: 0; }
  to { opacity: 1; }
}
.cov-date-body {
  background: #3F51B5;
  overflow: hidden;
  font-size: 16px;
  font-family: 'Roboto', Arial, sans-serif;
  font-weight: 400;
  position: fixed;
  display: block;
  width: 350px;
  max-width: 100%;
  z-index: 1052;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
  box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.2);
}
.cov-picker-box {
  background: #fff;
  width: 100%;
  display: inline-block;
  padding: 25px;
  box-sizing: border-box !important;
  -moz-box-sizing: border-box !important;
  -webkit-box-sizing: border-box !important;
  -ms-box-sizing: border-box !important;
  width: 350px;
  max-width: 100%;
  height: 280px;
  text-align: start!important;
}
.cov-picker-box td {
  height: 34px;
  width: 34px;
  padding: 0;
  line-height: 34px;
  color: #000;
  background: #fff;
  text-align: center;
  cursor: pointer;
}
.cov-picker-box td:hover {
  background: #E6E6E6;
}
.cov-date-body table {
  border-collapse: collapse;
  border-spacing: 0;
  width: 100%;
}
.cov-date-body td.day,
.cov-date-body tr.week th {
  width: 14.2857143%;
  text-align: center;
  height: 34px;
  padding: 0;
  line-height: 34px;
  color: #000;
  background: #fff;
  vertical-align: middle;
}
.cov-date-body td.day {
  cursor: pointer;
}
.cov-date-body th.week {
  background: transparent;
  font-weight: bold;
}
.cov-date-body .passive-day {
  color: #bbb;
}
.cov-date-body .checked {
  background: #F50057;
  color: #FFF !important;
  border-radius: 3px;
}
.cov-date-body .unavailable {
  color: #ccc;
  cursor: not-allowed;
}
.cov-date-monthly {
  height: 150px;
}
.cov-date-monthly > div {
  display: inline-block;
  padding: 0;
  margin: 0;
  vertical-align: middle;
  color: #fff;
  height: 150px;
  float: left;
  text-align: center;
  cursor: pointer;
}
.cov-date-previous,
.cov-date-next {
  position: relative;
  width: 20% !important;
  text-indent: -300px;
  overflow: hidden;
  color: #fff;
}
.cov-date-caption {
  width: 60%;
  padding: 50px 0!important;
  box-sizing: border-box;
  font-size: 24px;
}
.cov-date-caption span:hover {
  color: rgba(255, 255, 255, 0.7);
}
.cov-date-previous:hover,
.cov-date-next:hover {
  background: rgba(255, 255, 255, 0.1);
}
.cov-date-body .day:hover {
  background: #EAEAEA;
}
.cov-date-body .unavailable:hover {
  background: none;
}
.cov-date-body .checked:hover {
  background: #FF4F8E;
}

/* what is this for ??? */
.cov-date-next::before,
.cov-date-previous::before {
  width: 20px;
  height: 2px;
  text-align: center;
  position: absolute;
  background: #fff;
  top: 50%;
  margin-top: -7px;
  margin-left: -7px;
  left: 50%;
  line-height: 0;
  content: '';
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  transform: rotate(45deg);
}
.cov-date-next::after,
.cov-date-previous::after {
  width: 20px;
  height: 2px;
  text-align: center;
  position: absolute;
  background: #fff;
  margin-top: 6px;
  margin-left: -7px;
  top: 50%;
  left: 50%;
  line-height: 0;
  content: '';
  -webkit-transform: rotate(-45deg);
  -moz-transform: rotate(-45deg);
  transform: rotate(-45deg);
}
.cov-date-previous::after {
  -webkit-transform: rotate(45deg);
  -moz-transform: rotate(45deg);
  transform: rotate(45deg);
}
.cov-date-previous::before {
  -webkit-transform: rotate(-45deg);
  -moz-transform: rotate(-45deg);
  transform: rotate(-45deg);
}

.cov-vue-date {
  display: inline-block;
  color: #5D5D5D;
}

.button-box {
  background: #fff;
  vertical-align: top;
  height: 50px;
  line-height: 50px;
  text-align: right;
  padding-right: 20px;
}
</style>

<template>
  <div class="cov-vue-date" :class="option.wrapperClass ? option.wrapperClass : {}">

    <div class="datepicker-overlay" 
        v-if="showInfo.check" 
        @click="dismiss($event)" 
        v-bind:style="{'background' : option.overlayOpacity? 'rgba(0,0,0,'+option.overlayOpacity+')' : 'rgba(0,0,0,0.5)'}"
    >
      <div class="cov-date-body"
          ref="picker"
          role="application"
          aria-busy="false"
      >

        <div class="cov-date-monthly">
          <div class="cov-date-previous" tabindex="0" @click="nextMonth('pre')">
            <span class="sr-only"><slot name="gotoprev" Goto Previous Month</slot></span>
            <span aria-hidden="true">&lt;</span>
          </div>
          <div class="cov-date-caption" 
              :id="makeId('month')"
              role="heading"
              aria-live="assertive"
              aria-atomic="true"
          >
             <small>{{checked.year}}</small>
             <br>
             {{displayInfo.month}} {{checked.day}}
          </div>
          <div class="cov-date-next" tabindex="0" @click="nextMonth('next')">
            <span class="sr-only"><slot="gotonext">Goto Next Month</span></slot>
            <span aria-hidden="true">&gt;</span>
          </div>
        </div>

        <table 
            tabindex="0"
            role="grid"
            :aria-activedecendant="checked.id ? makeId('cell_' + checked.id) : ''"
            :aria-labeledby="makeId('month')"
        >
          <thead>
            <tr class="week" :id="makeId('weekdays')">
              <th v-for="(wday, wd) in library.week" :id="makeId('weekdays_' + (wd+1))">
                <abbr title="library.weekLong[wd]">{{ wday }}</abbr>
              </th>
            </tr>
          </thead>
          <tbody 
              ref="cal"
              @click="dateClick($event)"
              @keyup.left="moveLeft($event)"
              @keyup.right="moveRight($event)"
              @keyup.up="moveUp($event)"
              @keyup.down="moveDown($event)"
          >
           <tr v-for"w in 6" :id="makeId('row_' + w)">
              <td v-for="d in 7" 
                  tabindex="-1"
                  class="day"
                  role="gridcell"
                  :key="w+'_'+d"
                  :id="makeId('cell_' + getDay(w,d).id)"
                  :data-idx="getDay(w,d).id"
                  :headers="makeId('row_' + w) + ' ' + makeId('weekdays_' + d)"
                  :aria-selected="getDay(w,d).checked ? 'true' : 'false'"
                  :aria-disabled="getDay(w,d).unavailable ? 'true' : 'false'"
                  :class="{'checked':getDay(w,d).checked,'unavailable':getDay(w,d).unavailable,'passive-day': !(getDay(w,d).inMonth)}"
              >
                {{ getDay(w,d).value }}
              </td>
           </tr>
          </tbody>
        </table>

        <div class="button-box">
          <button tabindex="0" @click="showInfo.check=false" class="btn btn-default">
            <slot name="cancel">Cancel</slot>
          </button>
          <button tabindex="0" @click="picked" class="btn btn-default">
            <slot name="ok">Ok</slot>
          </button>
        </div>

      </div>
    </div>
  </div>
</template>

<script>
'use strict';

Object.defineProperty(exports, "__esModule", {
  value: true
});

var _moment = require('moment');

var _moment2 = _interopRequireDefault(_moment);

function _interopRequireDefault(obj) { return obj && obj.__esModule ? obj : { default: obj }; }

exports.default = {
  
  data: function data() {
    return {
      showInfo: {
        hour: false,
        day: false,
        month: false,
        year: false,
        check: false
      },
      displayInfo: {
        month: ''
      },
      library: {
        week: this.option.week,
        weekLong: this.option.weekLong,
        month: this.option.month,
        year: []
      },
      checked: {
        oldtime: '',
        currentMoment: null,
        year: '',
        month: '',
        day: '',
        hour: '00',
        min: '00',
        id: 0
      },
      dayList: [],
      selectedDays: []
    };
  },
  
  props: {
    required: false,
    value: { // For v-model
      type: String // yyyy-mm-dd format
    },
    // This will be replaced by above.  Need to parse on load/save
    date: {
      type: Object,
      required: true
    },
    // Change option to individual props for better binding
    option: {
      type: Object,
      default: function _default() {
        return {
          SundayFirst: true,
          // merge week & weekLong intarray of objects as weekdays
          week: ['Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa', 'Su'],
          weekLong: ['Momday', 'Tuesday', 'Wednesday', 'Thhursday', 'Friday', 'Saturday', 'Sunday'],
          month: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
          format: 'YYYY-MM-DD',
          wrapperClass: '',
          overlayOpacity: 0.5,
          dismissible: true
        };
      }
    },
    limit: {
      type: Array,
      default: function _default() {
        return [];
      }
    }
  },

  methods: {
    pad: function pad(n) {
      n = Math.floor(n);
      return n < 10 ? '0' + n : n;
    },
    
    makeId: function makeId(s) {
      return 'cov_' + this._uid + '_' + s;
    },
    
    // Simplify the moment2 calls into a helper function
    nextMonth: function nextMonth(type) {
      var next = (type === 'next') 
        ? (0, _moment2.default)(this.checked.currentMoment).add(1, 'M')
        : (0, _moment2.default)(this.checked.currentMoment).add(-1, 'M');
      this.showDay(next);
    },
    
    showDay: function showDay(time) {
      if (time === undefined || !(0, _moment2.default)(time, this.option.format).isValid()) {
        this.checked.currentMoment = (0, _moment2.default)();
      } else {
        this.checked.currentMoment = (0, _moment2.default)(time, this.option.format);
      }
      
      this.checked.year = (0, _moment2.default)(this.checked.currentMoment).format('YYYY');
      this.checked.month = (0, _moment2.default)(this.checked.currentMoment).format('MM');
      this.checked.day = (0, _moment2.default)(this.checked.currentMoment).format('DD');
      this.displayInfo.month = this.library.month[(0, _moment2.default)(this.checked.currentMoment).month()];

      // Build the daysList
      var days = [];
      var currentMoment = this.checked.currentMoment;
      var firstDay = (0, _moment2.default)(currentMoment).date(1).day();

      // gettting previous and next month
      // let currentMonth = moment(currentMoment)
      var previousMonth = (0, _moment2.default)(currentMoment).add(1, 'months');
      var nextMonth = (0, _moment2.default)(currentMoment).subtract(1, 'months');
      var monthDays = (0, _moment2.default)(currentMoment).daysInMonth();
      var oldtime = this.checked.oldtime;
      
      // Generate dayList entries for current month
      for (var i = 1; i <= monthDays; ++i) {
        days.push({
          value: i,
          inMonth: true,
          unavailable: false,
          checked: false,
          id: null,
          moment: (0, _moment2.default)(currentMoment).date(i)
        });
        if (i === Math.ceil((0, _moment2.default)(currentMoment).format('D'))
            && (0, _moment2.default)(oldtime, this.option.format).year() === (0, _moment2.default)(currentMoment).year()
            && (0, _moment2.default)(oldtime, this.option.format).month() === (0, _moment2.default)(currentMoment).month()) {
          days[i - 1].checked = true;
        }
      }
      
      // Add "passive" days at start of calendar list
      if (firstDay === 0) firstDay = 7;
      for (var _i = 0; _i < firstDay - (this.option.SundayFirst ? 0 : 1) + 7 ; _i++) {
        var passiveDay = {
          value: previousMonth.daysInMonth() - _i,
          inMonth: false,
          action: 'previous',
          unavailable: false,
          checked: false,
          id: null,
          moment: (0, _moment2.default)(currentMoment).date(1).subtract(_i + 1, 'days')
        };
        days.unshift(passiveDay);
      }
      
      if (this.limit.length > 0) {
        var _iteratorNormalCompletion = true;
        var _didIteratorError = false;
        var _iteratorError = undefined;

        try {
          for (var _iterator = this.limit[Symbol.iterator](), _step;
              !(_iteratorNormalCompletion = (_step = _iterator.next()).done);
              _iteratorNormalCompletion = true) {
            var li = _step.value;

            switch (li.type) {
              case 'fromto':
                days = this.limitFromTo(li, days);
                break;
              case 'weekday':
                days = this.limitWeekDay(li, days);
                break;
            }
          }
        } catch (err) {
          _didIteratorError = true;
          _iteratorError = err;
        } finally {
          try {
            if (!_iteratorNormalCompletion && _iterator.return) {
              _iterator.return();
            }
          } finally {
            if (_didIteratorError) {
              throw _iteratorError;
            }
          }
        }
      }
      
      // Add "passive" days at end of calendar list
      var passiveDaysAtFinal = 56 - days.length;
      for (var _i2 = 1; _i2 <= passiveDaysAtFinal; _i2++) {
        var _passiveDay = {
          value: _i2,
          inMonth: false,
          action: 'next',
          unavailable: false,
          checked: false,
          id: null,
          moment: (0, _moment2.default)(currentMoment).add(1, 'months').date(_i2)
        };
        days.push(_passiveDay);
      }
      
      // Add an ID for easy reference
      days.forEach(function (x, _i3) {
        x.id = _i3;
      });
      
      // Set the new day list
      this.dayList = days;
    },
    
    beforeUpdate: function() {
      this.$refs.picker.setAttribute('aria-busy','true');
    }.
    
    afterUpdate: function() {
      this.$refs.picker.setAttribute('aria-busy','false');
    },
    
    // Return a day object based on the week and day of week index
    getDay: function getDay(w,d) {
      var idx = w*7 + (d-1)
      return this.dayList[idx]
    },
    
    limitWeekDay: function limitWeekDay(limit, days) {
      days.map(function (day) {
        if (limit.available.indexOf(Math.floor(day.moment.format('d'))) === -1) {
          day.unavailable = true;
        }
      });
      return days;
    },
    
    limitFromTo: function limitFromTo(limit, days) {
      var _this2 = this;

      if (limit.from || limit.to) {
        days.map(function (day) {
          if (_this2.getLimitCondition(limit, day)) {
            day.unavailable = true;
          }
        });
      }
      return days;
    },
    
    getLimitCondition: function getLimitCondition(limit, day) {
      var tmpMoment = (0, _moment2.default)(this.checked.year + '-' + this.pad(this.checked.month) + '-' + this.pad(day.value));
      if (limit.from && !limit.to) {
        return !tmpMoment.isAfter(limit.from);
      } else if (!limit.from && limit.to) {
        return !tmpMoment.isBefore(limit.to);
      } else {
        return !tmpMoment.isBetween(limit.from, limit.to);
      }
    },
    
    clickDate: function(evt) {
      // future: var idx = element.dataset.idx;  Not suppoted on IE < 11
      // shim API available
      var idx = evt.target.getAttribute('data-idx');
      if (idx) {
        this.selectDay(this.dayList[parseInt(idx,10)]);
      }
    },

    keyLeft: function moveLeft(evt) {
      this.selectDay(this.checkd.id - 1]);
    },

    keyRight: function moveRight(evt) {
      this.selectDay(this.checkd.id + 1]);
    },
    
    keyUp: function moveUp(evt) {
      this.selectDay(this.checkd.id - 7]);
    },

    keyDown: function moveDown(evt) {
      this.selectDay(this.checkd.id + 7]);
    },
    
    selectDay: function(obj) {
      if (obj.unavailable || obj.value === '') {
        return false;
      }
      if (!obj.inMonth) {
        this.nextMonth(obj.action);
      }
      this.dayList.forEach(function (x) {
        x.checked = false;
      });
      this.checked.day = this.pad(obj.value);
      this.checked.id = obj.id;
      obj.checked = true;
      // We want the user to click the "OK" button to select  
      // this.picked();
    },
    
    showCheck: function showCheck() {
      if (this.date.time === '') {
        this.showDay();
      } else {
        this.checked.oldtime = this.date.time;
        this.showDay(this.date.time);
      }
      this.showInfo.check = true;
    },
    
    picked: function picked() {
      var ctime = this.checked.year + '-' + this.checked.month + '-' + this.checked.day + ' ' + this.checked.hour + ':' + this.checked.min;
      this.checked.currentMoment = (0, _moment2.default)(ctime, 'YYYY-MM-DD HH:mm');
      this.date.time = (0, _moment2.default)(this.checked.currentMoment).format(this.option.format);
      this.showInfo.check = false;
      this.$emit('change', this.date.time);
    },
    
    dismiss: function dismiss(evt) {
      if (evt.target.className === 'datepicker-overlay') {
        if (this.option.dismissible === undefined || this.option.dismissible) {
          this.showInfo.check = false;
          this.$emit('cancel');
        }
      }
    }
    
  }
};
</script>
