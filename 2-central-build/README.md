# 2. Central Build

This option centralizes the build and image location of Drupal, allowing individual teams to simply source the centrally managed Drupal image from a well known location.

First, create the Drupal CI/CD project/namespace:

```
oc new-project drupal-cicd
```

Next, deploy the CI/CD pipeline and trigger the build.


```
oc apply -f 2-central-build/cicd/

oc create -f 2-central-build-pipeline-run/run-build.yaml 
```

Once the build is complete, you can deploy Drupal to a new namespace.  You will have to grant the `default` service account in the new namespace `system:image-puller` on the `drupal-cicd` project in order for it to be able to pull the image from that project.

```
oc new-project drupal-dev
oc adm policy add-role-to-user system:image-puller system:serviceaccount:drupal-dev:default -n drupal-cicd
```

Finally, you can deploy Drupal:

```
oc apply -f 2-central-build/drupal/
```

Once Drupal has started, you can either complete the install manually by clicking on the route and following the instructions, or you can use the Job to run `drush` to complete the install:

```

```

Once the build completes it will deploy the new image.  You can then click on the Drupal route in order to finish the install manually, or you can create a `Job` to do this for you automatically.  The `Job` uses the Drupal Shell (drush).  It will take 5-10min for Drupal to finish installing.  The `Job` pod will turn green when it is complete.

```
oc apply -f 1-all-in-one/drush-install-job
```

This can be repeated in any new namespace/project.  However, it means each "Team" needs to manage the lifecycle of their own Drupal images.  This has pros and cons.
