# Portland Oregon

Portland efforts by http://hackoregon.org.

This directory contains the customizations and settings required to deploy the 
broadband test site for Portland, Oregon.

## Git Workflow and Contributing

We are attempting to maintain consistency with the main Seattle project and
periodically pull in changes into our fork.  The following is a summary of our
branching and workflow conventions.

 - ```master```: is used only to pull in changes from opentechinstitute/piecewise
 - ```portland```: is the new 'default' branch for hackoregon/broadbandmap-piecewise
 - ```portland_<feature-or-username>```: feature branch where project members develop

To participate please clone this repository locally.  Create a new branch and 
name it something like ```portland_myname```.  Make your changes and commit them.

Push your branch to the hackoregon/broadbandmap-piecewise repository.  Use the
GitHub web interface to submit a pull request to hackoregon/broadbandmap-piecewise.

Take care that you are not submitting a pull request to the opentechinstitute
repository.

### Pulling Changes from Upstream

Periodically we will want to pull changes from the upstream opentechinstitute
repository.  When we do this we'll coordinate to collapse all of our feature branches
into the main portland branch finishing up work.  Any branches not ready to merge
we will need to identify and take special actions to cherry-pick commits from them
later.

After branches have been merged or identified for later cherry-picking we will
pull changes from upstream master into local master.  We'll then rebase those
changes into the portland branch.  All of our commits in the portland branch will
then have new hashes after rebasing.

At this point we would need to test everything and once verified we would be free
to fix the branches that need cherry-picking and to create new feature branches to
continue work.

## Google Developer Console

UPDATEME

## M-Labs

UPDATEME

## Portland Specific Customizations

UPDATEME

## Deploying Portland Site With Ansible

We have created a copy of all the ansible tasks for the project starting with
```00_playbook.yml```.  We'll refine as we go.  We'll need to pay attention to
changes in upstream.

Please see ```03_portland_tasks.yml``` for Portland specifics.  We are attempting to 
organize the files in a way that we can just deploy the entire directories over the 
top of the main project files for a "Portland" deployment.

portland/piecewise/client_secrets.json must be manually placed in the repo prior to
deployment.

These things need to be done on the server after Ansible has deployed the site.

* Ingest bigquery data and aggregate it
    * ```$ cd /opt/piecewise```
    * ```$ sudo python -m piecewise.ingest```
* Check log file for errors...
    * ```$ tail -200f /var/log/piecewise/uwsgi.log```

## Updating a Deployed Server

This will work for Vagrant or a deployed system like EC2

SSH into the server and su to the root user or a user who can sudo
(e.g. the 'vagrant' user is just fine).

```
cd /opt/piecewise.git
sudo git fetch origin
sudo git pull origin HEAD
sudo ansible-playbook -i "localhost," -c local portland/00_playbook.yml
```

If you are only using Vagrant locally you should be able to update the install with...

```
vagrant provision
```

This will bring the git repository current with the remote; then run the ansible
playbook again to update the system.
