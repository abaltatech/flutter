# README_ABALTATECH.md

## Overview

This document outlines how we maintain and apply custom modifications to the Flutter engine within our fork. It serves as a guide for developers who need to create and validate changes to the fork. We have done changes only to the iOS Flutter engine.

## Structure of Changes

Our modifications to the Flutter engine are stored as patch files within the repository. Applying multiple patches is done in lexicographic order and thus the files have a consecutive number as a prefix to their name in order to be applied in the correct order. These patch files are created using standard Git commands. The patch files are located in the `master` branch under the `abaltatech_patches` directory.

## Applying Patches Locally

When working on a local machine, developers should apply the patches in the order that they were created before proceeding with the standard Flutter engine build process.

- For a single patch:

  ```sh
  git apply 000XX-my-changes.patch
  ```

- For multiple patch files:

  ```sh
  git am *.patch
  ```

After applying the patches the engine can be compiled by following the official Flutter documentation for [Compiling the Flutter Engine](./engine/src/flutter/docs/contributing/Compiling-the-engine.md).

## Creating and Committing Changes

After creating and validating changes locally, developers should generate a patch from their modifications and commit it as a separate file within the `abaltatech_patches` directory on the `master` branch. The patch file should follow the ordering convention where the next consecutive number is added as a prefix to the name of the patch file.

- To create a patch from unstaged changes:

  ```sh
  git diff > 000XX-my-new-change.patch
  ```

- To create a patch from a commit:

  ```sh
  git format-patch -1 HEAD
  ```

After that proceed to creating a pull request to the `master` branch with the patch file.

## Verifying Changes

When a pull request is created, the CI pipeline builds a custom iOS Flutter engine with the applied patches on top of the `master` branch. The resulting build is uploaded and can be used to test the changes in the relevant repository.

Once the changes are verified, the pull request can be merged into `master`.

## Releasing a Stable Version

After merging the changes into `master`, a developer must trigger a manual workflow to create a release with the merged changes. This is done by manually starting the workflow **TBD**, which takes a release reference as an input argument and builds the Flutter engine with the patches from `master` applied on top of the specified release ref.

This release is considered stable and should be used by our applications.
