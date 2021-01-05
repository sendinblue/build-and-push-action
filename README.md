# Build and Push Action

This action performs build and push of the image to [GCR]. Particularly, it:
- performs login to [GCR] using [JSON key file](https://cloud.google.com/container-registry/docs/advanced-authentication) method (if JSON key provided),
- derives the proper image tag from the current branch name/Git tag, esp. 
    - removes forbidden characters (e.g. slashes) in branch names, 
    - removes `v` prefix in tags,
- builds the image using a _Dockerfile_ in the root folder, and
- pushes the image to [GCR].

## Inputs

### `image-name`

**Required** The name of the image to build, e.g. `example-app`.

### `gcp-project-id`

**Required** ID of the project in [GCP](https://cloud.google.com/resource-manager/docs/creating-managing-projects), e.g. `my-project-1234`.

### `gcp-service-account-key`

Optional JSON key to get access to [GCP].

## Outputs

### `image`

Full image path in [GCR], e.g. `gcr.io/my-project-1234/example-app:1.0.0`.

### `image-tag`

Tag of the image, e.g. `1.0.0`.

## Example usage

    uses: sendinblue/build-and-push-action@main
    with:
        image-name: 'example-app'
        gcp-project-id: 'my-project-1234'

[GCR]: https://cloud.google.com/container-registry
[GCP]: https://cloud.google.com/
