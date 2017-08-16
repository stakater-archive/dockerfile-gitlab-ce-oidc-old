# dockerfile-gitlab-ce-oidc

Inspirations from https://github.com/ComputerScienceHouse/gitlab-ce-oidc

The above repo uses a omniauth-openid-connect gem (https://github.com/jjbohn/omniauth-openid-connect) which is not 
being maintained any more; and this fork https://github.com/m0n9oose/omniauth_openid_connect is the most maintained one right now.

This repository serves to add OpenID Connect support to the official GitLab Docker image. The resulting image, which is
automatically built when the upstream gitlab/gitlab-ce image is updated, can be found on the Docker Hub.

OmniAuth is a Ruby authentication framework aimed to abstract away the difficulties of working with various types of 
authentication providers. It is meant to be hooked up to just about any system, from social networks to enterprise 
systems to simple username and password authentication.

https://github.com/omniauth/omniauth/wiki

Ruby gem omniauth_openid_connect

https://rubygems.org/gems/omniauth_openid_connect

## OpenID Connect (OIC)

OpenID Connect (OIC) is a simple identity layer on top of the OAuth 2.0 protocol. It allows clients to verify the 
identity of the end-user based on the authentication performed by KeyCloak, as well as to obtain basic profile 
information about the end-user in an interoperable and REST-like manner. OIC performs many of the same tasks as OpenID 2.0,
but does so in a way that is API-friendly, and usable by native and mobile applications.

## Configuration

To use this image, add the following options to your GITLAB_OMNIBUS_CONFIG environment variable, replacing the noted 
variables with the appropriate values from your IdP:

```
gitlab_rails['omniauth_enabled'] = true;
gitlab_rails['omniauth_allow_single_sign_on'] = true;
gitlab_rails['omniauth_block_auto_created_users'] = false;
gitlab_rails['omniauth_auto_sign_in_with_provider'] = '<PROVIDER_NAME>';
gitlab_rails['omniauth_providers'] = [{'name'=>'openid_connect', 'args'=>{'name'=>'<PROVIDER_NAME>', 'scope'=>['openid', 'profile'], 'response_type'=>'code', 'discovery'=>true, 'issuer'=>'<ISSUER_URL>', 'client_options'=>{'port'=>'443', 'scheme'=>'https', 'host'=>'<IDP_HOSTNAME>', 'identifier'=>'<CLIENT_ID>', 'secret'=>'<CLIENT_SECRET>', 'redirect_uri'=>'https://<GITLAB_URL>/users/auth/<PROVIDER_NAME>/callback'}}}];
```
---

```
config.omniauth :openid_connect, {
name: :openid_connect,
scope: [:openid, :profile],
response_type: :code,
client_options: {
port: 8081,
scheme: "https",
host: "myprovider.com",
identifier: "clientID",
secret: "clientSecret",
redirect_uri: "http://myapp.com/users/auth/openid_connect/callback",
},
}
```

The name must be openid_connect and scopes are the minimal ones required.

