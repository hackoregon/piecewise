# Portland Example

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

## Ansible Tasks Specific to Portland

These things need to be done on the server after Ansible has deployed the site.

Please see ```portland_tasks.yml``` for specifics.

* Ingest bigquery data and aggregate it
    * $ cd /opt/piecewise
    * $ sudo python -m piecewise.ingest

* Put center.js where bq2geojson can find it
    * $ cd /opt/piecewise
    * $ python portland_example/portland_center.py /opt/bq2geojson/html/js/center.js
