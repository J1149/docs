# PAI Messages

PAI Messages is a system in PAI Pass that allows users internal to PAI Pass and to developers using PAI Pass. It allows for:

  - real-time messaging 
  - third-party developers to use it as the the messaging system for their third-party app; which allows for:
      - filtering of messages dependent on what the conversation is about

    
It uses websockets to do this real time messages. 

## Third-Party Usage

To use this the developer needs to wrap

```
https://paipass.p19dev.com/pai-messages/
```

in an iframe. If you are using Django, you might do it like so,

```djangotemplate
{% block content %}
    <div id="pai-messages-iframe-div"
         class="pai-messages-iframe-div">
    </div>
    <input type="hidden" id="PAIPASS_URL" name="variable" value="{{ PAIPASS_URL }}">
    {{ thread|json_script:"thread-data" }}
    {{ application|json_script:"application-data" }}
{% endblock %}
```

and have javascript that looks like,

```javascript
const thread = JSON.parse(document.getElementById('thread-data').textContent);
const application = JSON.parse(document.getElementById('application-data').textContent);
const URL_BASE = document.getElementById('PAIPASS_URL').value;
console.log('URL_BASE', URL_BASE)
const PaiMsgsZoidComponent = zoid.create({

    // The html tag used to render my component

    tag: 'pai-msgs-component',

    // The url that will be loaded in the iframe or popup, when someone includes my component on their page

    url: new URL(`${URL_BASE}/pai-messages`, window.location.href).href,
    dimensions: {
        width: '100%',
        height: '100%',
    },
    props: {
        thread: {
            type: 'object',
        },
        application: {
            type: 'object',
        }
    }
});
PaiMsgsZoidComponent({thread: thread, application: application}).render('#pai-messages-iframe-div')
```

where,

- PAIPASS_URL=https://paipass.p19dev.com/pai-messages/
- thread 
- application

The corresponding code for this can be found here,

- [pai_messages.html](https://github.com/J1149/catena/blob/master/backend/django_messages/templates/django_messages/pai_messages.html)
- [index.js](https://github.com/J1149/catena/blob/master/backend/static_content/assets/index.js)