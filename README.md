# VueJs-Notification-Service
This is a vueJs notification service 
it includes :
error,
success,
information and warning message.

For this service i have used `vue-notification` package.

Install

`npm install --save vue-notification`

in main.js
``` javascript
import Vue           from 'vue'
import Notifications from 'vue-notification'

/*
or for SSR:
import Notifications from 'vue-notification/dist/ssr.js'
*/

Vue.use(Notifications)
```
in App.vue file add this component at the end 
``` javascript 
        <notifications position="top right" width="35%">
      <template slot="body" slot-scope="props">
        <div class="vue-notification notification"
             :class="[props.item.type]" @click="popupClicked(props)">
          <a class="title">{{props.item.title}}</a>
          <div class="subtitle" v-html="props.item.text"></div>
        </div>
      </template>
    </notifications>
```

Also add this method into methods section
``` javascript
 popupClicked(notificationInstance) {
        notificationInstance.close();
      }
```

Here is the notificationservice.js file:


``` javascript

const notificationService = {
    success: (message) => {
        vueInstance.$notify({
            duration: 5000,
            type: 'success',
            title: 'Success',
            text: message
        });
    },

    warning: (message) => {
        vueInstance.$notify({
            duration: 5000,
            type: 'warn',
            title: 'Warning',
            text: message
        });
    },

    info: (message) => {
        vueInstance.$notify({
            duration: 5000,
            title: 'Info',
            text: message
        });
    },

    chat: (title, message, data) => {
        vueInstance.$notify({
            title,
            duration: 15000,
            text: message,
            data
        });
    },

    error: (error) => {
        if (typeof error === 'string') {
            showError(error);
            return;
        }
        if (error.body) {
            error = error.body.error;
        }
        if (error.data) {
            error = error.data;
        }
        if (typeof error.message === 'string') {
            showError(error.message);
            return;
        }
        Object.keys(error.message).forEach((key) => {
            if (typeof error.message[key] === 'string') {
                showError(error.message[key]);
            } else {
                error.message[key].forEach((message) => {
                    showError(message);
                });
            }
        });
    }
};
