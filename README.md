# Moonlight
RSS Announcement generator for Moonraker


## Registering a repo

Announcement registration is open to Moonraker clients and projects
that could be described as part of the "Klipper ecosystem".  When
a repo is registered with Moonlight it is possible to deliver
announcements to users by creating issues in a repo's issue tracker.

At this time projects must meet the following requirements:

- Have a user base of at least 200 users
- Have at least one stable release
- Have been in development for at least 6 months with consistent activity
- Forks of Klipper, unofficial extras, and repos that contain only
  configuration are not eligible.
- Only one project per GitHub user/organization may be registered

These requirements may be relaxed in the future as we are able to gauge
how the current process scales.  Its possible that the way Moonraker
announcements are created, generated and received by instances of Moonraker
will change over time, thus it is desirable to limit the amount of
registered repos to something manageable.

To register a repo, create a pull request that adds your repo info
to `src/config.json`.

```json
{
    "moonraker": {
        "repo_owner": "Arksine",
        "repo_name": "moonraker",
        "description": "API Host For Klipper",
        "authorized_creators": ["Arksine"]
    },
    "klipper": {
        "repo_owner": "Klipper3d",
        "repo_name": "klipper",
        "description": "A 3D Printer Firmware",
        "authorized_creators": ["KevinOConnor"]
    }
    // Add your repo info here
}
```
Entries should be submitted in the following format, see below
for an explanation for each field:

```json
{
    "project name" : {
        "repo_owner": "GitHub Username or Organization",
        "repo_name": "Name of the repo on GitHub",
        "description": "A brief description of the project",
        "authorized_creators": [
            "A list of GitHub user names authorized to create announcements on this repo"
        ]
    }
}
```

The `project_name` is the name that will be assigned to your feed, generally
this will match the `repo_name`, but it isn't a requirement.

Once your repo is registered you should create `announcement` and `critical`
labels in your repo.  When an authorized GitHub user creates an issue
tagged with `announcement` it will be eligible for Moonlight's issue parser
and added to your projects announcement feed. Issues tagged with both the
`announcement` and `critical` labels will be assigned a high priority.
High priority announcements should be rare, the typical use case is to notify
users of a situation that must be addressed as soon as possible.

When an issue is closed it is removed from the RSS feed.  Closed issues should
not be reopened.  Likewise, once the `announcement` label has been applied it
should not be removed.  Moonlight has a limit of up to 20 announcements per
repo, when this limit has been reached old announcements will be removed from
the feed.

For users of your project to receive announcements through moonraker they
must opt in to your feed by
[configuring your feed](https://moonraker.readthedocs.io/en/latest/configuration/#announcements)
in `moonraker.conf`:

```ini
# moonraker.conf

[announcements]
subscriptions:
  project_name
```

Announcements should be used to notify users of updates to your project.
This includes upcoming releases, status updates, and dependency issues,
and critical vulnerabilities.  Best practice is to refrain
from creating announcements for other projects in the Klipper ecosystem,
as this may potentially result in duplicate announcements.
