# Test List
A list of steps for testing the workflow's features.

## Deleting branch skips workflow

### Steps
1. Create a new branch.
1. Delete the branch.

### Output
1. Workflow triggers.
1. Workflow skipped.

## Creating a new tag creates a corresponding major tag

### Steps
1. Create a new tag in the format `v<Major>.<Minor>[.<Patch>]`. For example, `v0.1.0`, `v0.2.0`, `v1.0.2`.

### Output
1. Workflow triggers.
1. Workflow creates a new major tag with a revision matching the tag created earlier.

## Creating a tag that is not the latest short-circuits

### Steps
1. Create another tag based on the one created earlier.

### Output
1. Workflow triggers.
1. Upgrade major tag short-circuits because of equality.

## Deleting major tag skips workflow

### Steps
1. Delete the major tag created earlier.

### Output
1. Workflow triggers.
1. Workflow skipped.

## Deleting tag while major does not exist short-circuits

### Steps
1. Delete one of the tags created earlier.

### Output
1. Workflow triggers.
1. Downgrade major tag short-circuits because major tag doesn't exist.

## Cleanup

### Steps
1. Create new tags under one major version.
1. Create another tag based on the latest tag.

## Deleting tag which results in latest revision not changing short-circuits

### Steps
1. Delete one of the tags created earlier based on the latest tag.

### Outputs
1. Workflow triggers.
1. Downgrade major tag short-circuits because the major tag's revision will not change.

## Deleting latest tag downgrades major tag to the next latest tag

### Steps
1. Delete the latest tag of one major version.

### Output
1. Workflow triggers.
1. Downgrade major tag updates major tag to next latest version.

## Deleting all tags under a major version deletes the major tag

### Steps
1. Delete all tags under a major version.

### Output
1. Workflow triggers.
1. Major tag is deleted because no versions exist under that major version.

## Check extraction of major tag is correct

### Steps
1. Find logs of the following.
  - Creation of a tag through pushing. Example information.
    - Major tag: `v0`
    - Tag: `v0.1.0`
    - Tag Path: None
    - Version: `v0.1.0`
  - Deletion of a tag through pushing. Example information.
    - Major tag: `v1`
    - Tag: `v1.2.0`
    - Tag Path: None
    - Version: `v1.2.0`
  - Deletion of a tag through GitHub GUI. Example information.
    - Major tag: `a/b/v2`
    - Tag: `a/b/v2.3.0`
    - Tag Path: `a/b/`
    - Version: `v2.3.0`
1. Confirm information is correct.

### Outputs
N/A

## Test tags with directories

### Steps
1. Repeat the previous tests but with tags inside directories. Name one of the directories with one or more periods; for example, `Test.App/v1.2.0`
