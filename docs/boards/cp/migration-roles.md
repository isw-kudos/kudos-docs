# Migrated role comparison

When migrating from activities, the permissions will be maintained although in some cases it may not look exactly the same, below are some examples of permissions set in Activities and their equivalent in Boards / Activities Plus.

| Type                    | Activities                   | Boards                    |
| ----------------------- | ---------------------------- | ------------------------- |
| User                    | Owner / Author / Reader      | Owner / Author / Reader   |
| (Shared with) Community | Owner / Author / Reader      | Owner / Author / Reader   |
| (Owned By) Community    | Allow all as owner           | Community is set to Owner |
| (Owned By) Community    | Allow all as Author / Reader | ???                       |
| (Owned By) Community    | Allow only named members as Owner / Author / Reader      | Community is set to "Community Owners only" (Community owners are board owners), named members are added to board with Owner / Author / Reader, other Community members will see this board in the list but not be able to view it.
