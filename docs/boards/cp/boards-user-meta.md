### Boards User Data
This process will migrate all user preferences data from Kudos Boards Websphere. 

Each user who has used Kudos Boards Websphere is likely to have created some of this data. It includes:
- The labels a user has assigned to colours which they apply to Board Tiles.
- The Catagories a user has created which they apply to Board Tiles.

If the user already exists in Kudos Boards Docker:
- Their color labels will be deleted and replaced with the labels from Boards Websphere.
- Imported Categories will be added to their existing list of categories.

Subsequent runs of this process will import any data for new Boards Websphere users and overwrite the previously imported data from the last run.