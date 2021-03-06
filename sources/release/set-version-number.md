page_main_title: Setting version number
main_section: CD
sub_section: Managing release versions
page_title: Setting the version number for a Release
page_description: How to set the version number for a Release in Shippable

# Setting the version number for a Release

-  Create a version resource in the shippable.yml file. Specify your initial version in the versionName field.

```
resources:
  # Version resource
  - name: release-version
    type: version
    seed:
      versionName: "1.0.0"
```

- Create a release job in the shippable.yml file. Specify the version resource and your manifest or deploy jobs as inputs. In this example
 we provide a single manifest job as an input.

```
jobs:
  #Manifest job  
  - name: java-img-manifest
    type: manifest
    steps:
      - IN: ecr-img
      - IN: ecr-img-opts

  #Release job    
  - name: release-job
    type: release
    steps:
      - IN: java-img-manifest
      - IN: release-version
```

- Running the release job will set the current version to 1.1.0, incrementing the minor version. To increment other components of the version, such as major or patch, please see the section on incrementing version numbers.

## Improve this page

We really appreciate your help in improving our documentation. If you find any problems with this page, please do not hesitate to reach out at [support@shippable.com](mailto:support@shippable.com) or [open a support issue](https://www.github.com/Shippable/support/issues). You can also send us a pull request to the [docs repository](https://www.github.com/Shippable/docs).
