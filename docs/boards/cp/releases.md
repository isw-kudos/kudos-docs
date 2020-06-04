## Kudos Boards for HCL Connections CP

[Guide to upgrade from CP to Dockerhub images](https://docs.kudosapps.com/boards/cp/dockerhub/)

---

#### 2020-04-09

[Dockerhub](https://hub.docker.com/repository/docker/iswkudos/kudos-boards/tags?page=1&name=2020-04-09)

Images:

```
iswkudos/kudos-boards:user-2020-04-09
iswkudos/kudos-boards:provider-2020-04-09
iswkudos/kudos-boards:licence-2020-04-09
iswkudos/kudos-boards:notification-2020-04-09
iswkudos/kudos-boards:webfront-2020-04-09
iswkudos/kudos-boards:core-2020-04-09
iswkudos/kudos-boards:boards-2020-04-09
```

Fixes:

- Connections OAuth issue - missing scope

---

#### 2020-03-06

[Dockerhub](https://hub.docker.com/repository/docker/iswkudos/kudos-boards/tags?page=1&name=2020-03-06)

Images:

```
iswkudos/kudos-boards:user-2020-03-06
iswkudos/kudos-boards:provider-2020-03-06
iswkudos/kudos-boards:licence-2020-03-06
iswkudos/kudos-boards:notification-2020-03-06
iswkudos/kudos-boards:webfront-2020-03-06
iswkudos/kudos-boards:core-2020-03-06
iswkudos/kudos-boards:boards-2020-03-06
```


Fixes:

- Updating cards permissions
- Boards list - show completed & deleted
- individual import of Activity with emails
- member issue when moving card into new board
- Archived cards appear twice
- Powered by Kudos image
 
Language support:
```
  "supported": {
    "ar":[],
    "bg":[],
    "ca":[],
    "cs":[],
    "da":[],
    "de": [],
    "el":[],
    "en": ["US"],
    "es":[],
    "fi":[],
    "fr":[],
    "he":[],
    "hr":[],
    "hu":[],
    "it":[],
    "ja":[],
    "kk":[],
    "ko":[],
    "nb":[],
    "nl":[],
    "pl":[],
    "pt":[],
    "ro":[],
    "ru":[],
    "sk":[],
    "sl":[],
    "sv":[],
    "th":[],
    "tr":[],
    "zh":["TW"]
  },
    "default": "en"
```

---

#### 2020-06-04

[Dockerhub](https://hub.docker.com/repository/docker/iswkudos/kudos-boards/tags?page=1&name=2020-06-04)

Images:

```
iswkudos/kudos-boards:user-2020-06-04
iswkudos/kudos-boards:provider-2020-06-04
iswkudos/kudos-boards:licence-2020-06-04
iswkudos/kudos-boards:notification-2020-06-04
iswkudos/kudos-boards:webfront-2020-06-04
iswkudos/kudos-boards:core-2020-06-04
iswkudos/kudos-boards:boards-2020-06-04
```

Please see our [Cloud blog](https://blog.kudosapps.com/weve-got-some-kudos-boards-changes-for-you)

Improvements:
- Loading performance
- Rendering performance
- Reduce size of application
- Node view UI refresh

New Features:
- Card theme from uploaded images
- Preview uploaded files (images, docx, pdf, html etc)
- Todos Overview - [filtering to selected Boards](https://blog.kudosapps.com/part-3-weve-got-some-kudos-boards-changes-for-you)
- Drag and drop Email into Cards (ie from HCL Notes)
- Activity Stream Gadget for Boards - [config updates required](/boards/connections/widgets-on-prem/)
- Multiple Assignment options for Cards

Fixes:
- Email notifications for invited collaborators