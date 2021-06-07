# OpenShift Template

Templates allow you to create catalog entries for easy "self service" in OpenShift.  Templates are easy to create, since they are just a list of Kubernetes resources that can be parameterized.  Templates are, however, OpenShift specific.  It's only the template yaml file itself that is OpenShift specific.  All of the resources a template contains are of course reusable and portable (except for OpenShift-specific concepts like Routes).

By default, a Template will only be accessible from the Project it is created in.  For example, if you create this template in the "drupal" project, then you will only have access to this template from within that project.

However, if an admin creates a template in the `openshift` project, then it becomes accessible to everyone through the default catalog.

To add this Drupal template to the global OpenShift catalog, run:

```
oc apply -f 4-openshift-templaten -n openshift
```

To test out the template, from the OpenShift Developer perspective:

1. Create a new project.
2. Click on the "From Catalog" tile.
3. Search for "drupal", then click on the Drupal tile and "Instantiate Template".
4. You can keep the default options, or change them if you like.
5. You need to set **Application Namespace/Project** to the same value as your current namespace (there's no easy way to do this in a template).
6. Scroll to the bottom and click **Create**.

This will create the database and app deployments, the install job, the pipeline, and the first pipeline run.  In a few minutes drupal shoud be up and running.

