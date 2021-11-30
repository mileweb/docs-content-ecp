# Managing Artifacts Under a Repository

An artifact represents a unique build of container image. An artifact is created when you run “docker build” in your docker environment to push a new image to ECP registry. Artifacts are stored and managed under a repository.

The following procedure describes how to view artifacts for a repository, and how to view artifact details.

1. In the left pane, click **Image Registry > Registry Projects**.
2. On the Registry Projects page, click the name of a project. The details page appears.
3. To view artifacts for a repository, click a number in the **Artifacts** column within the **Repository** area at the bottom of the page.
   <p align=center><img src="/docs/resources/images/registry/edit-project-artifacts.png" width="600">

   The page opened shows a list of artifacts under the repository.
   <p align=center><img src="/docs/resources/images/registry/artifacts-list.png" width="600">

   The **Actions** drop-down list on each row has options to copy digest of an artifact and delete an artifact. Mousing over the **Vulnerability** column allows you to view a summary of the artifact's vulnerabilities report.

4. To view details of an artifact, click the **artifact** column on the artifacts list page to go to a details page.
   <p align=center><img src="/docs/resources/images/registry/artifact-details.png" width="600">

| **Fields**   | **Description**                                                                                           |
| :----------: | --------------------------------------------------------------------------------------------------------- |
| 1            | The Tags area shows a list of tags pointing to the same artifact. A tag is a convenient alias used to refer to an artifact. The **Actions** drop-down list on each row has options to delete a tag and to deploy an application using the tag.                |
| 2            | The Overview area shows some summary information about the artifact.                                                  |
| 3            | The Vulnerabilities area shows a list of vulnerabilities reported for the artifact. To view more information about a vulnerability, click the **Vulnerability** column.  |