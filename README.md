# vue-datepicker-aria
ARIA compliant Datepicker component for Vue.js 2.2.x

**Note:** This repo is currently in development and is not complete!

# Demo

The demo page is [HERE](http://hilongjw.github.io/vue-datepicker/demo.html).

![Screenshot](screenshot.png)

# Requirements

- [Vue.js](https://github.com/yyx990803/vue) `^2.2.0`
- [moment](https://github.com/moment/moment) `^2.11.1`

# Installation

## npm

```shell
$ npm install vue-datepicker-aria
```

# Usage

```html
<script>
// for Vue 2.0
import myDatepicker from 'vue-datepicker'

export default {
  data () {
    return {
      startTime: {
        time: ''
      },
      endtime: {
        time: ''
      }

      option: {
        type: 'day',
        week: ['Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa', 'Su'],
        month: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
        format: 'YYYY-MM-DD',
        overlayOpacity: 0.5, // 0.5 as default
        dismissible: true // as true as default
      },
      timeoption: {
        type: 'min',
        week: ['Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa', 'Su'],
        month: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
        format: 'YYYY-MM-DD HH:mm'
      },
      limit: [{
        type: 'weekday',
        available: [1, 2, 3, 4, 5]
      },
      {
        type: 'fromto',
        from: '2016-02-01',
        to: '2016-02-20'
      }]
    }
  },
  components: {
    'date-picker': myDatepicker
  }
}
</script>
<template>
  <div class="card">

    <!-- for Vue 2.0 -->
    <div class="row">
      <span>Departure Date：</span>
      <date-picker :date="startTime" :option="option" :limit="limit"></date-picker>
    </div>

  </div>
</template>
```

# API

 - Option 

 * format

```
format: 'YYYY-MM-DD HH:mm'
```
Note HH:mm will lways be zero

 * week

```
 week: ['Mo', 'Tu', 'We', 'Th', 'Fr', 'Sa', 'Su']
 weekLong: ['Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday', 'Sunday']
```

 * month

```
  month: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August','September', 'October', 'November', 'December']
```

* wrapperClass

```
wrapperClass: ''
```

 * animate

```
  overlayOpacity: 0.5, // 0.5 as default
  dismissible: true // as true as default
```


 - limit

  * from sometime to sometime(when from/to is empty, days before/after end/start time will be available)

```javascript

limit: {
  type:'fromto',
  from:'2016-01-10',
  to:'2017-01-30'
}

```
 * weekdays

```javascript

limit:{
  type: 'weekday',
  available: [1, 2, 3, 4, 5] 
}

```

### prop


* Vue 2.0

```javascript
date: {
  time: '' // string
}
```

```html

<date-picker :date="date" :limit="limit"></date-picker>

```


# License

[The MIT License](http://opensource.org/licenses/MIT)

