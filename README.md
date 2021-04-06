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

### `image-tag`

Set image tag explicitly. Default: derived from the Git tag or `latest` if on master/main branch.

### `registry`

Registry domain. Default: `gcr.io`.

### `gcp-project-id`

ID of the project in [GCP](https://cloud.google.com/resource-manager/docs/creating-managing-projects), 
e.g. `my-project-1234`. Default: `.project_id` from the JSON key (`gcp-service-account-key` input).

### `gcp-service-account-key`

JSON key to get access to [GCP].

### `dockerfile`

Name of the Dockerfile to use. Default: `./Dockerfile`.

### `build-options`

Additional options to pass to docker build command.

### `build-path`

Location of the build context for the docker build command. Default: `.`.

### `use-buildkit`

Flag whether to use BuldKit. Set to `1` to enable DOCKER_BUILDKIT flag.

## Outputs

### `image`

Full image path in the registry, e.g. `gcr.io/my-project-1234/example-app:1.0.0`.

### `image-tag`

Tag of the image, e.g. `1.0.0`.

### `image-digest`

Digest of the image, e.g. `sha256:8414aa82208bc4c2761dc149df67e25c6b8a9380e5d8c4e7b5c84ca2d04bb244`.

### `image-full-name`

Full image name (without the tag), e.g. `gcr.io/my-project-1234/example-app`.

## Example usage

    uses: sendinblue/build-and-push-action@main
    with:
        image-name: 'example-app'
        gcp-project-id: 'my-project-1234'

[GCR]: https://cloud.google.com/container-registry
[GCP]: https://cloud.google.com/
