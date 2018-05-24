## run-parts

[![Build Status](https://travis-ci.org/Oefenweb/ansible-run-parts.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-run-parts) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-run--parts-blue.svg)](https://galaxy.ansible.com/Oefenweb/run-parts)

Manage `run-parts` (and scripts) in Debian-like systems.

#### Requirements

* `run-parts` (will be installed)

#### Variables

* `run_parts_groups`: [default: `{}`]: Scripts declarations
* `run_parts_groups.key`: [required]: The name of the script (e.g. `last-backup`)
* `run_parts_groups.key.pre`: [optional, default `[]`]: Pre sync commands
* `run_parts_groups.key.rsync`: [required]: Rsync declarations
* `run_parts_groups.key.rsync.src`: [required]: The source directory
* `run_parts_groups.key.rsync.dest`: [required]: The destination directory
* `run_parts_groups.key.rsync.options`: [optional, default `[]`]: Options (e.g. `['--aP', '--delete']`)
* `run_parts_groups.key.rsync.time`: [optional, default `false`]: Whether or not to time the `rsync` command
* `run_parts_groups.key.post`: [optional, default `[]`]: Post sync commands

* `run_parts_jobs`: [default: `[]`]: Sync jobs (scheduled by `cron.d`)
* `run_parts_jobs.{n}.name`: [required]: Description of a crontab entry, should be unique, and changing the value will result in a new cron task being created (e.g. `last-backup`)
* `run_parts_jobs.{n}.job`: [required]: The command to execute (e.g. `/usr/local/bin/last-backup`)
* `run_parts_jobs.{n}.state`: [default: `present`]: Whether to ensure the job is present or absent
* `run_parts_jobs.{n}.day`: [default: `*`]: Day of the month the job should run (`1-31`, `*`, `*/2`)
* `run_parts_jobs.{n}.hour`: [default: `*`]: Hour when the job should run (e.g. `0-23`, `*`, `*/2`)
* `run_parts_jobs.{n}.minute`: [default: `*`]: Minute when the job should run (e.g. `0-59`, `*`, `*/2`)
* `run_parts_jobs.{n}.month`: [default: `*`]: Month of the year the job should run (e.g `1-12`, `*`, `*/2`)
* `run_parts_jobs.{n}.weekday`: [default: `*`]: Day of the week that the job should run (e.g. `0-6` for Sunday-Saturday, `*`)

## Dependencies

None

#### Example(s)

##### ...

```yaml
---
- hosts: all
  roles:
   - run-parts
```

#### License

MIT

#### Author Information

Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-run-parts/issues)!
