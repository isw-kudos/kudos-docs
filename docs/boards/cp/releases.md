## Huddo Boards for HCL Connections CP

[Guide to upgrade from CP to Dockerhub images](https://docs.huddo.com/boards/cp/dockerhub/)


### Update Notes:
**Note: As of 2020-09-18 all updates must use the new Helm chart**

Please use the appropriate update command. For example:

Huddo Boards in Kubernetes
```
helm upgrade boards https://docs.huddo.com/assets/config/kubernetes/kudos-boards-4.0.0.tgz -i -f ./boards.yaml --namespace boards --recreate-pods
```

Component Pack (Activities Plus)
```
helm upgrade kudos-boards-cp https://docs.huddo.com/assets/config/kubernetes/kudos-boards-cp-2.0.0.tgz -i -f ./boards-cp.yaml --namespace connections --recreate-pods
```

---

#### 2020-10-14
[Dockerhub](https://hub.docker.com/repository/docker/iswkudos/kudos-boards/tags?page=1&name=2020-10-14)

Images:

```
iswkudos/kudos-boards:user-2020-10-14
iswkudos/kudos-boards:provider-2020-10-14
iswkudos/kudos-boards:licence-2020-10-14
iswkudos/kudos-boards:notification-2020-10-14
iswkudos/kudos-boards:webfront-2020-10-14
iswkudos/kudos-boards:core-2020-10-14
iswkudos/kudos-boards:boards-2020-10-14
iswkudos/kudos-boards:activity-migration-2020-10-14
```

Improvements:

- Updated Rich Text Editor

Fixes:

- Re-open last board view
- User trial reminder
- Extension of user trials
- Download linked files with .odt extension

---

#### 2020-10-05
[Dockerhub](https://hub.docker.com/repository/docker/iswkudos/kudos-boards/tags?page=1&name=2020-10-05)

Images:

```
iswkudos/kudos-boards:user-2020-10-05
iswkudos/kudos-boards:provider-2020-10-05
iswkudos/kudos-boards:licence-2020-10-05
iswkudos/kudos-boards:notification-2020-10-05
iswkudos/kudos-boards:webfront-2020-10-05
iswkudos/kudos-boards:core-2020-10-05
iswkudos/kudos-boards:boards-2020-10-05
iswkudos/kudos-boards:activity-migration-2020-10-05
```

Features:

- Board Search
    - Increase visibility of filters
    - Maintain filters after page reload
    - Hide Completed Todos
    - Hide Empty Lists
- Preview Files, support for
    - Excel (xlsx, xls)
    - PDF

Improvements:

- Rich Text Editor - allow indenting paragraphs
- Logging updates
- Activity Migration - add default link type

Fixes:

- Default handling of links from migrated Activities
- User Avatar initials fallback
- Include current user as option in user licence search & custom field person

---

#### 2020-09-18
[Dockerhub](https://hub.docker.com/repository/docker/iswkudos/kudos-boards/tags?page=1&name=2020-09-18)

Images:

```
iswkudos/kudos-boards:user-2020-09-18
iswkudos/kudos-boards:provider-2020-09-18
iswkudos/kudos-boards:licence-2020-09-18
iswkudos/kudos-boards:notification-2020-09-18
iswkudos/kudos-boards:webfront-2020-09-18
iswkudos/kudos-boards:core-2020-09-18
iswkudos/kudos-boards:boards-2020-09-18
iswkudos/kudos-boards:activity-migration-2020-09-18
```

Features:

- New rich text editor with improved handling for
    - tables
    - whitepace
    - paste from office
    - font, font size, font color
    - file upload feedback
- Search Board by Custom Fields (Text & People)
- Search improvements - show sub-tasks when parent match filter

Improvements:

- UI feedback for Chrome Incognito third-party security exception
- Microsoft Teams file preview
- Microsoft Teams file links
- Internal microservice communication (**Note**: this requires a new Helm Chart V2)
- Updated HCL Connections icon

Fixes:

- Issue where page reloads constantly in Connections frame
- Outlook integration issue
- File Preview in Safari
- Board Properties toolbar 'more' menu
- API update for completing a task already completed


---

#### 2020-08-24

[Dockerhub](https://hub.docker.com/repository/docker/iswkudos/kudos-boards/tags?page=1&name=2020-08-24)

Images:

```
iswkudos/kudos-boards:user-2020-08-24
iswkudos/kudos-boards:provider-2020-08-24
iswkudos/kudos-boards:licence-2020-08-24
iswkudos/kudos-boards:notification-2020-08-24
iswkudos/kudos-boards:webfront-2020-08-24
iswkudos/kudos-boards:core-2020-08-24
iswkudos/kudos-boards:boards-2020-08-24
iswkudos/kudos-boards:activity-migration-2020-08-24
```

Features:

- Live Board Tile views (my/public/groups)
- Export Board/Cards as CSV
- Upload multiple files at once
- Drag and drop multiple emails into an open card
- Link to Board/List/Card - copies a direct URL to clipboard

Improvements:

- Performance (loading times)
- Use local font files (no external URLs)
- Focused people search results in Connections
- Previewing linked files has link to Connections file info
- Loading Community images
- Support nested comments imported from Activities
- Support pasting images in comments
- Support long board names in left sidenav
- Scroll members area in right sidenav when long
- Show summary numbers in Members dialog
- UI feedback while saving custom fields
- Cookie handling (SameSite)
- Firefox scrollbar styling

Fixes:

- Saving of description on reload & modal change
- Comment duplicate while saving
- Support non-english @mentions
- @mention overflow issue
- Recent boards in left sidenav
- Move and not open page crash issue
- Ordering of links in a card
- Sharing my private file with a public folder
- Previewing of linked Community files
- Activities imported with unknown user assignments
- Dragging color onto tiles
- Allow unassigning users who are no longer members
- Ordering issue on cards created using past
---

#### 2020-07-10

[Dockerhub](https://hub.docker.com/repository/docker/iswkudos/kudos-boards/tags?page=1&name=2020-07-10)

Images:

```
iswkudos/kudos-boards:user-2020-07-10
iswkudos/kudos-boards:provider-2020-07-10
iswkudos/kudos-boards:licence-2020-07-10
iswkudos/kudos-boards:notification-2020-07-10
iswkudos/kudos-boards:webfront-2020-07-10
iswkudos/kudos-boards:core-2020-07-10
iswkudos/kudos-boards:boards-2020-07-10
iswkudos/kudos-boards:activity-migration-2020-07-10
```

Improvements:

- Activity Stream deep-linking to Community Boards
- Community Boards - open board links in fullpage
- Fix searching individual Activity imports
- Update individual Activity import grouping of top level entries
- Fix loading of some imported Activities

Activity Migration:

- Support migration of Activity files with unicode & whitespace characters in name
- Performance & stability improvements (large activities & filesets, rollback files on failure, extra logging, retry logic)

---

#### 2020-06-17

[Dockerhub](https://hub.docker.com/repository/docker/iswkudos/kudos-boards/tags?page=1&name=2020-06-17)

Images:

```
iswkudos/kudos-boards:user-2020-06-17
iswkudos/kudos-boards:provider-2020-06-17
iswkudos/kudos-boards:licence-2020-06-17
iswkudos/kudos-boards:notification-2020-06-17
iswkudos/kudos-boards:webfront-2020-06-17
iswkudos/kudos-boards:core-2020-06-17
iswkudos/kudos-boards:boards-2020-06-17
iswkudos/kudos-boards:activity-migration-2020-06-17
```

Fixes:

- Show newly created comments in Todo view
- Support Activity URL redirects
- Community Boards loading issue

Activity Migration:

- UI control options fix
- Support migration of Activity files with special characters in name
- Support for Activity links
- Protect against system tenant IDs '-Ignore-Organization-ID-' etc
- DB2 support for PEOPLEDB on secondary host

---

#### 2020-06-05

[Dockerhub](https://hub.docker.com/repository/docker/iswkudos/kudos-boards/tags?page=1&name=2020-06-05)

Images:

```
iswkudos/kudos-boards:user-2020-06-05
iswkudos/kudos-boards:provider-2020-06-05
iswkudos/kudos-boards:licence-2020-06-05
iswkudos/kudos-boards:notification-2020-06-05
iswkudos/kudos-boards:webfront-2020-06-05
iswkudos/kudos-boards:core-2020-06-05
iswkudos/kudos-boards:boards-2020-06-05
```

Please see our [Cloud blog](https://blog.huddo.com/weve-got-some-kudos-boards-changes-for-you)

Improvements:

- Loading performance
- Rendering performance
- Reduce size of application
- Node view UI refresh

New Features:

- Card theme from uploaded images
- Preview uploaded files (images, docx, pdf, html etc)
- Todos Overview - [filtering to selected Boards](https://blog.huddo.com/part-3-weve-got-some-kudos-boards-changes-for-you)
- Drag and drop Email into Cards (ie from HCL Notes)
- Activity Stream Gadget for Boards - [config updates required](/boards/connections/widgets-on-prem/)
- Multiple Assignment options for Cards

Fixes:

- Email notifications for invited collaborators

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
- Powered by Huddo image
 
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
