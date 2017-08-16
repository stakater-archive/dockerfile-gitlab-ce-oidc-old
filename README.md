# dockerfile-gitlab-ce-oidc

Inspirations from https://github.com/ComputerScienceHouse/gitlab-ce-oidc

The above repo uses a omniauth-openid-connect gem (https://github.com/jjbohn/omniauth-openid-connect) which is not 
being maintained any more; and this fork https://github.com/m0n9oose/omniauth_openid_connect is the most maintained one right now.

This repository serves to add OpenID Connect support to the official GitLab Docker image. The resulting image, which is
automatically built when the upstream gitlab/gitlab-ce image is updated, can be found on the Docker Hub.

## Configuration

To use this image, add the following options to your GITLAB_OMNIBUS_CONFIG environment variable, replacing the noted 
variables with the appropriate values from your IdP:

