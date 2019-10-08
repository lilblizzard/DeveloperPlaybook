# Guide for Infrastructure Team First Responder

The DLSS infrastructure team is using a rotating role of "first responder".  This doc explains a bit about the concept of
the first responder role and then outlines specific duties and expectations.

PRs to this doc are always welcome, but especially while we're ironing things out and having regular retrospectives about the process.  If it sticks, and/or the access team adopts it, we can get rid of this caveat.

## Table of Contents

* ["First Responder" Rotation Premises](#first-responder-rotation-premises)
  * ["First responder" != "on call"](#first-responder--on-call)
* [Duties](#duties)
  * [Weekly Dependency Updates](#weekly-dependency-updates)
    * [Ensure dependency update spreadsheet is created](#ensure-dependency-update-spreadsheet-is-created)
    * [Ensure Monday dependency updates are completed](#ensure-monday-dependency-updates-are-completed)
      * [Code that isn't a Ruby Application or Gem](#code-that-isnt-a-ruby-application-or-gem)
  * [Verify / Notify Coverage for Following Week](#verify--notify-coverage-for-following-week)
  * [Sign Up for Your Next First Responder Shift](#sign-up-for-your-next-first-responder-shift)
  * [Proactively Check for Production Problems](#proactively-check-for-production-problems)
  * [Triage Production Problems](#triage-production-problems)
  * [Improve Troubleshooting Documentation as Needed](#Improve-Troubleshooting-Documentation-as-Needed)
  * [Improve First Responder Instructions as Needed](#improve-first-responder-instructions-as-needed)
  * [Other Duties as Assigned](#other-duties-as-assigned)
* [How to Proactively Check for Production Problems](#how-to-proactively-check-for-production-problems)
* [How to Triage Production Problems](#how-to-triage-production-problems)
  * [A note on prioritization](#a-note-on-prioritization)
* [What if first responder isn't available?](#what-if-first-responder-isnt-available)

# "First Responder" Rotation Premises

* Respond to production issues in a timely fashion during business hours.
* Single process for handling questions outside the team's current work cycle.
* Share the responsibility for production outages across the team in a planned way.
* Every team member rotates through this responsibility.
* Encourage cross-training, since a first-responder will likely have to investigate applications with which they are unfamiliar.
* Shore up missing and outdated documentation of production code and processes for everyone (ops, devops, PSM, stakeholders, devs, etc), informed by actual attempts to find and use said documentation to investigate production issues.

### "First Responder" != "On Call"

* The idiosyncratic name of the role is intentional.  It is not the duty of the "first responder" to be on-call outside of the first responder's normal work hours (which may not line up exactly with business hours in Palo Alto).  The first responder rotation is an effort to watch and triage production issues in an intentional and organized fashion, since no engineer was officially assigned this responsibility in the past, and such minding of things was haphazard.

# Duties

## Weekly Dependency Updates

### Ensure dependency update spreadsheet is created

Instructions are here https://docs.google.com/spreadsheets/d/1LysSAPFsRGt9PteWpVswp74xnPXyLLxADpHRfh69VLQ/edit#gid=0

It *may* be that someone in a time zone further east than Palo Alto has already done this, but it is the first responder's responsibility to ensure this gets done.

### Ensure Monday dependency updates are completed

It is a team task to complete these updates, but the first responder needs to make sure that all codebases needing updates have updates merged and deployed.  Note that some projects need to have PRs created by hand ("Manually clone and update repos that failed bundle update" on line 6 of instructions). It may be helpful to post in channel how many updates each developer should do, given who is working that day and how many PRs there are.

#### Code that isn't a Ruby Application

We have code bases to maintain that aren't Ruby applications or gems.  We have not yet tackled how to deal with these.

- javascript node apps with npm updates:
  - https://github.com/sul-dlss/access-update-scripts has code to create PRs for npm package updates, but it currently only works for the sul-dlss github organization.  All the sinopia code is in the LD4P github organization.  Should make a maintenance ticket to address this?
- java code
- other

Note that security updates affecting our ruby gems will be caught when doing capistrano deployments via `gemfile audit`.

## Verify / Notify Coverage for Following Week

1. Verify first responder for following week is still able to cover it.  Check this with on deck person on Monday (and keep in mind throughout the week, e.g. if person becomes ill).  (schedule: https://docs.google.com/spreadsheets/u/1/d/13TJR93Yc9_eF5B7w4XDx6ggG_wb3aLkgCHjpLwmHPBA/)
  1. It's the scheduled responder's responsibility to find a swap, not current first responder. _TBD: We'll figure something out if said responder is unavailable due to emergency?_
  1. The person covering the following week is "on deck" for this week.
1. Set Slack reminders in `#dlss-infrastructure` for next week's Monday morning. The reminders should indicate who is first responder and who is on deck for that week, and should be set for 3 am Pacific time/6 am Eastern, so that the east coast early risers don't have to wait for it.
  * documentation on Slack's `/remind` command:  https://get.slack.help/hc/en-us/articles/208423427-Set-a-reminder
    * e.g. if Alice and Bob are up next week, `/remind #dlss-infrastructure on Monday at 3 am "@alice is the first responder this week, and @bob is on deck"`

## Sign Up for Your Next First Responder Shift

The infrastructure team has 8 developers, so you should be taking a shift every 8 or so weeks.
* schedule:  https://docs.google.com/spreadsheets/u/1/d/13TJR93Yc9_eF5B7w4XDx6ggG_wb3aLkgCHjpLwmHPBA/

## Proactively Check for Production Problems

See [How to Proactively Check for Production Problems](#how-to-proactively-check-for-production-problems) section below for specifics.

## Triage Production Problems

If a user reports a problem, or if one is surfaced from monitoring, the first responder is meant to timebox an investigation of the problem (_TBD: 30 min?_).  See [How to Triage Production Problems](#how-to-triage-production-problems) section below for more specifics.

## Improve Troubleshooting Documentation as Needed

If you need to triage or troubleshoot a problem and realize some documentation is missing, please provide it.  List of appropriate places:
* https://github.com/sul-dlss/DevOpsDocs - e.g. what an ops or devops person would need to know to handle the situation
* README or other top level markdown doc in codebase (viewable via github)
  * Which codebase would need to be apparent from the problem
* Wiki for the codebase
* ? - in general, just try to consider where the person interested in the info might look first.  A user might go to the wiki, a dev might go to the README, ops folks might head to DevOpsDocs.  Use your best judgement and ask for feedback if unsure.

The above documents should be useful and current.  Please submit improvements as PRs for review.

If for some reason documentation is a significant undertaking, the call for documentation can be filed as an issue and prioritized/resourced by management.

## Improve First Responder Instructions as Needed

We need this document to be useful and current.  Please submit improvements as PRs for review.

## Other Duties as Assigned

* Management may choose to have the first responder handle a non-project work ticket
  * If so, ensure you assign the ticket to yourself and put it in the "in progress" column the project board https://github.com/orgs/sul-dlss/projects/1
* First responder may be asked to spearhead a work estimate https://github.com/sul-dlss-labs/estimation (note that these are, by definition, meant to be done by more than one person; if it's smaller, should it be a ticket in a project?)

# How to Proactively Check for Production Problems

At the very least, the first responder should be watching incoming alerts from Honeybadger.  (https://app.honeybadger.io/projects)

Other places to monitor:
* Nagios alerts (https://sul-nagios-prod.stanford.edu/nagios/  The Services tab on the left column will give overview of checks.  The Problems->Services tab will give you what’s alerting.)
* feedback email lists, e.g. argo-feedback, sinopia-feedback, etc
* the `#dlss-infrastructure` channel
* the `#sul-cap-collab` channel, which has developers in the School of Medicine working on the Profiles project (which we connect to with our sul-pub system)
* Slack channels relevant to applications in the portfolio, e.g. `#pre-assembly`
* Resque dashboards  e.g.
  - robots
    - https://robot-console-prod.stanford.edu/overview
      - https://robot-console-prod.stanford.edu/failed
    - https://argo.stanford.edu/report/workflow_grid
  - pre-assembly
    - https://sul-preassembly-prod.stanford.edu/resque/overview
  - preservation
    - https://preservation-catalog-prod-01.stanford.edu/resque/overview
      - https://preservation-catalog-prod-01.stanford.edu/resque/failed
* cron daemon emails
* Github security alerts
* If you hear about possible security issues through other avenues (e.g. `#iso-public` on Slack, your consumption of the news in general), and you feel that the issues may be relevant and uncaptured, file an issue and call attention to it as needed.

# How to Triage Production Problems

If a user reports a problem, or if one is surfaced from monitoring, the first responder is meant to timebox an investigation of the problem (_TBD: no more than 30 min?_).  It's fine to ask teammates with relevant expertise for help, but also think about what documentation is needed so the next person will need less help. It is _not_ the job of the first responder to fix the issue on the spot (though if the fix is trivial, it's fine to do so).

* All problems investigated should get a ticket UNLESS:
  * Investigation leads to discovery that there is no problem
    * If additional documentation would have made this clearer, then
      * First responder creates additional documentation (preferred) or a ticket for it
  * Fixing the problem will be as quick as writing up a ticket
    * First responder fixes the problem in this case.
* All new tickets should be added to the infrastructure team's [general project board](https://github.com/orgs/sul-dlss/projects/1) (select project board from "projects" when on issue page)

![Add to infrastructure project board](images/add_to_infra_proj_board.png)

### A note on prioritization

Prioritization is the responsibility of management, not the responsibility of the first responder.  Though of course, if a developer becomes aware of what may be a high priority issue, and is unsure whether management is aware of the issue (or sufficiently aware of its severity), the developer is certainly encouraged to bring the issue to their manager's attention.

* Types of data to help with prioritization
  * Is this a significant production problem? A non-critical outage?
  * Is there a workaround?  If so, how onerous is it?  How adequately does it cover the unavailable or misbehaving functionality?
  * Does it affect lots of end-users?  A handful of super-users?
  * How many digital resources are affected?
  * Is it blocking time sensitive work?

# What if first responder isn't available?

The idea is for the first responder to be "interruptible" for production problems during his/her week of coverage.  If there are significant blocks of time when this isn't true (e.g. ½ day meeting with no access to slack or email), or if life happens (illness, family emergency, etc.), hopefully the first responder can arrange for coverage.  ("I'll take one of your days if you can cover Tues for me").  Please notify `#dlss-infrastructure` Slack channel of changes.

When the first responder can't arrange for coverage, the default would be for the "on deck" responder to become first responder.  The "on deck" person is the first responder for the following week.