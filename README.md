## run-parts

[![Build Status](https://travis-ci.org/Oefenweb/ansible-run-parts.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-run-parts)
[![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-run--parts-blue.svg)](https://galaxy.ansible.com/Oefenweb/run-parts)

Manage `run-parts` (and scripts) in Debian-like systems.

#### Requirements

* `debianutils` (will be installed)
* `cron` (will be installed)

#### Variables

* `run_parts_groups`: [default: `[]`]: Group declarations (e.g. directories)
* `run_parts_groups.{n}.name`: [required]: Name (e.g. `lorem`, will result in the directory `/etc/run-parts/lorem.d`)
* `run_parts_groups.{n}.owner`: [optional, default `root`]: The name of the user that should own the directory
* `run_parts_groups.{n}.group`: [optional, default `root`]: The name of the group that should own the directory
* `run_parts_groups.{n}.mode`: [optional, default `0755`]: The UNIX permission mode bits of the directory
* `run_parts_groups.{n}.parts`: [optional, default `[]`]: Part declarations (e.g. files)
* `run_parts_groups.{n}.parts.{m}.name`: [required]: Name (e.g. `00-ipsum`)
* `run_parts_groups.{n}.parts.{m}.content`: [optional, default `''`]: (File) content
* `run_parts_groups.{n}.owner`: [optional, default `root`]: The name of the user that should own the file
* `run_parts_groups.{n}.group`: [optional, default `root`]: The name of the group that should own the file
* `run_parts_groups.{n}.mode`: [optional, default `0755`]: The UNIX permission mode bits of the file
* `run_parts_groups.{n}.parts.{m}.state`: [optional, default `present`]: State
* `run_parts_groups.{n}.state`: [optional, default `present`]: State

* `run_parts_jobs`: [default: `[]`]: Sync jobs (scheduled by `cron.d`)
* `run_parts_jobs.{n}.name`: [required]: Description of a crontab entry, should be unique, and changing the value will result in a new cron task being created (e.g. `lorem.d`)
* `run_parts_jobs.{n}.job`: [required]: The command to execute (e.g. `run-parts /etc/run-parts/lorem.d`)
* `run_parts_jobs.{n}.state`: [default: `present`]: Whether to ensure the job is present or absent
* `run_parts_jobs.{n}.day`: [default: `*`]: Day of the month the job should run (`1-31`, `*`, `*/2`)
* `run_parts_jobs.{n}.hour`: [default: `*`]: Hour when the job should run (e.g. `0-23`, `*`, `*/2`)
* `run_parts_jobs.{n}.minute`: [default: `*`]: Minute when the job should run (e.g. `0-59`, `*`, `*/2`)
* `run_parts_jobs.{n}.month`: [default: `*`]: Month of the year the job should run (e.g `1-12`, `*`, `*/2`)
* `run_parts_jobs.{n}.weekday`: [default: `*`]: Day of the week that the job should run (e.g. `0-6` for Sunday-Saturday, `*`)

#### Dependencies

None

#### Example(s)

```yaml
---
- hosts: all
  roles:
   - run-parts
  vars:
    run_parts_groups:
      - name: lorem
        parts:
          - name: 00-ipsum
            content: |
              #!/usr/bin/env bash
              echo "${0}" $(( ( RANDOM % 10 ) + 1 ));
          - name: 01-dolor
            content: |
              #!/usr/bin/env bash
              echo "${0}" $(( ( RANDOM % 10 ) + 1 ));

      - name: sit
        parts:
          - name: 00-amet
            content: |
              #!/usr/bin/env bash
              echo "${0}" $(( ( RANDOM % 10 ) + 1 ));
          - name: consectetur
            state: absent

      - name: adipiscing
        state: absent

    run_parts_jobs:
    - name: lorem.d
      job: run-parts /etc/run-parts/lorem.d
      minute: '@daily'
```

#### License

MIT

#### Author Information

Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-run-parts/issues)!
