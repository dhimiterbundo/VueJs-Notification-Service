# VueJs-Notification-Service
This is a vueJs notification service 
it includes :
error,
success,
information and warning message.

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
