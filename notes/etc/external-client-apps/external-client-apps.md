# External Client Apps
Framework to connect Salesforce data into third-party applications. 

- Fully metadata-compliant
- Include structural improvements to maintain separate user roles and allow second-generation managed packaging.


## ECA Metadata Architecture

Salesforce has redesigned the architecture of External Connected Apps to be more modular, more granular, and better for source control.

External Client Apps are broken down into three main metadata components:

1. `ExternalClientApplication`

    Defines the External Client App.

    - Label

    - API name

    - Contact email

    - Type of distribution

2. `ExternalClientAppOauthSettings`

    The OAuth configuration for the External Client App.

    - Enabled Authentication flows

    - OAuth scopes

    - Callback URL

    - Signing Certificate

    - Secret configuration (requirements, PKCE, etc)

3. `ExternalClientAppOauthPolicies`

    Specifies the OAuth policies applied to the External Client App.

    - IP relaxation
    
    - Permitted users

    - Refresh token policy

    - Session policies


In addition to the ECA-specific metadata, there is an Org-wide OAUth settings metadata file that needs to be created for the Org prior to deploying an ECA:

- `OauthCustomScope`

    Global OAuth configuration applied to the Org.

    - Token lifetime
    
    - Allowed OAuth flows that can be used by External Client Apps in the Org

    - CORS

    - Trusted origins


## Connected Apps vs External Client Apps

External Client Apps (ECA) are the next-generation of Connected Apps.


### Feature Comparison

| Feature | Connected Apps | External Client Apps |
|---|---|---|
| 2GP Packaging | [Restricted](https://developer.salesforce.com/docs/atlas.en-us.pkg2_dev.meta/pkg2_dev/sfdx_dev_dev2gp_connected_app.htm) (1) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.configure_packageable_external_client_apps.htm&language=en_US&type=5) |
| 1GP Packaging | [Available](https://developer.salesforce.com/docs/atlas.en-us.pkg1_dev.meta/pkg1_dev/connected_apps.htm) | Not available |
| Distribution state management | Not available | [Available](https://help.salesforce.com/s/articleView?id=xcloud.configure_packageable_external_client_apps.htm&language=en_US&type=5) |
| Distinct developer and admin user roles | Not available | [Available](https://help.salesforce.com/s/articleView?id=xcloud.external_client_apps.htm&language=en_US&type=5) |
| Subscriber association and disassociation | Not available | [Available](https://help.salesforce.com/s/articleView?id=xcloud.associate_and_disassociate_external_client_apps.htm&language=en_US&type=5) |
| Salesforce Setup UI | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_create_basics.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.create_a_local_external_client_app.htm&language=en_US&type=5) |
| Metadata API | [Restricted](https://developer.salesforce.com/docs/atlas.en-us.api_meta.meta/api_meta/meta_connectedapp.htm) (2) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.meta_external_client_apps_creation.htm&language=en_US&type=5) |
| OAuth 2.0 | [Available](https://help.salesforce.com/s/articleView?id=xcloud.remoteaccess_authenticate.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.external_client_apps_oauth_flow_config.htm&language=en_US&type=5) (3) |
| SAML | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_create_saml_sso.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.configure_external_client_app_saml.htm&language=en_US&type=5) |
| OpenID Connect | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_create_openid_connect.htm&language=en_US&type=5) | Available |
| OAuth consumer key and consumer secret rotation | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_rotate_consumer_details.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.eca_stage_oauth_credentials.htm&language=en_US&type=5) |
| Trusted IP Range for OAuth Web Server Flow | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_edit_ip_ranges.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.meta_configure_external_client_app_oauth_settings.htm&language=en_US&type=5) |
| Copy when cloning a sandbox | Available | [Available](https://help.salesforce.com/s/articleView?id=xcloud.external_client_apps.htm&language=en_US&type=5) (4) |
| API access control | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_manage.htm&language=en_US&type=5) | Not needed (5) |
| Custom attribute creation | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_edit_custom_attributes.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.configure_custom_attributes_for_external_client_apps.htm&language=en_US&type=5) |
| Audit support | [Available](https://help.salesforce.com/s/articleView?id=xcloud.admin_monitorsetup.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.admin_monitorsetup.htm&language=en_US&type=5) |
| Logging support | [Available](https://help.salesforce.com/s/articleView?id=xcloud.admin_monitorsetup.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.admin_monitorsetup.htm&language=en_US&type=5) |
| Start URL management | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_manage_start_url.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.manage_eca_start_url.htm&language=en_US&type=5) |
| OAuth access policy management | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_manage_oauth.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.manage_external_client_apps.htm&language=en_US&type=5) |
| IP relaxation | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_continuous_ip.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.manage_external_client_apps.htm&language=en_US&type=5) |
| Session policy management | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_manage_session_policies.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.manage_external_client_apps.htm&language=en_US&type=5) |
| Mobile policy management | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_manage_mobile.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.configure_external_client_app_mobile_settings_policies.htm&language=en_US&type=5) |
| Custom handler management | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_manage_custom_handler.htm&language=en_US&type=5) | [Available](https://developer.salesforce.com/docs/atlas.en-us.apexref.meta/apexref/apex_class_Auth_ExternalClientAppOauthHandler.htm) |
| User provisioning | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_user_provisioning.htm&language=en_US&type=5) | Not available |
| OAuth usage management | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_manage_current_sessions.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.manage_external_client_app_usage.htm&language=en_US&type=5) |
| Profile management | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_manage_additional_settings.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=platform.admin_userprofiles.htm&language=en_US&type=5) |
| Permission set management | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_manage_additional_settings.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.manage_external_client_apps.htm&language=en_US&type=5) |
| Data access management (OAuth) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_manage.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.meta_configure_external_client_app_policies.htm&language=en_US&type=5) |
| Canvas | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_create_canvas.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.configure_external_client_app_canvas.htm&language=en_US&type=5) |
| Notifications | [Available](https://help.salesforce.com/s/articleView?id=xcloud.connected_app_notifications.htm&language=en_US&type=5) | [Available](https://help.salesforce.com/s/articleView?id=xcloud.configure_external_client_app_notification_settings.htm&language=en_US&type=5) |


## Setting Up An External Client App

### Secure Unnattended Machine-to-Machine Connections

This section applies only for connecting third-party systems to consume Salesforce data using secure machine-to-machine credentials using a non-interactive OAuth authentication flow.
