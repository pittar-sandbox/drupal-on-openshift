# 1. All-In-One Approach

First, create a new Project/Namespace:

```
oc new-project all-in-one
```

Next, deploy Drupal resources (it won't finish starting, since Drupal hasn't been built yet).

If you chose a differnt namespace, you will have to update the image reference in the app deployment to use the proper namespace:

```
        - image: image-registry.openshift-image-registry.svc:5000/all-in-one-test/drupal-wxt:latest
```

Then, install the Drupal resources.

```
oc apply -f 1-all-in-one
```

Run the first build (either through the OpenShift UI, or by running the following command).

```
oc create -f 1-all-in-one-pipeline-run/run-build.yaml
```

Once the build completes it will deploy the new image.  You can then click on the Drupal route in order to finish the install manually, or you can create a `Job` to do this for you automatically.  The `Job` uses the Drupal Shell (drush).  It will take 5-10min for Drupal to finish installing.  The `Job` pod will turn green when it is complete.

```
oc apply -f 1-all-in-one/drush-install-job
```

This can be repeated in any new namespace/project.  However, it means each "Team" needs to manage the lifecycle of their own Drupal images.  This has pros and cons.
