# Vuejs-memo

# Vue Component Datepicker 
- Html Template
```
  <script type="text/x-template" id="date-picker">
      <input placeholder="YYYY-MM-DD" style="width: 100%" type="text">
  </script>
```

- Javascript
```
    Vue.component('datepicker', {
        props: ['value'],
        template: '#date-picker',
        mounted: function () {
            var vm = this;
            $(this.$el).datepicker({
                dateFormat: 'yy-mm-dd',
                onSelect: function(dateText) {
                    vm.$emit('input', dateText);
                }
            });
        },
        watch: {
            value: function (value) {
                // update value
                $(this.$el).val(value)
            }
        },
        destroyed: function () {
            //$(this.$el).off().select2('destroy')
        }
    });
```

- html
```
<datepicker v-bind:value="value" v-model="value"></datepicker>
```

# Vue Component Select2
- Html Template
```
    <script type="text/x-template" id="select2-template">
        <select style="width: 100%">
            <slot></slot>
        </select>
    </script>
```

- Javascript
```
    Vue.component('select2', {
        props: ['options', 'value'],
        template: '#select2-template',
        mounted: function () {
            var vm = this;
            $(this.$el)
            // init select2
                .select2({ data: this.options })
                .val(this.value)
                .trigger('change')
                // emit event on change.
                .on('change', function () {
                    vm.$emit('input');
                });
        },
        watch: {
            value: function (value) {
                // update value
                $(this.$el).val(value)
            },
            options: function (options) {
                // update options
                $(this.$el).empty().select2({ data: options })
            }
        },
        destroyed: function () {
            $(this.$el).off().select2('destroy')
        }
    });
```

- Html
```
 options = [
    {
        id: 0,
        text: 'enhancement'
    },
    {
        id: 1,
        text: 'bug'
    },
    {
        id: 2,
        text: 'duplicate'
    },
    {
        id: 3,
        text: 'invalid'
    },
    {
        id: 4,
        text: 'wontfix'
    }
  ];

    <select2 :options="options" v-model="idValue">
    </select2>
```
