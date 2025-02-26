---
title: Accessing the management console
intro: '{% data reusables.enterprise_site_admin_settings.about-the-management-console %}'
redirect_from:
  - /enterprise/admin/articles/about-the-management-console
  - /enterprise/admin/articles/management-console-for-emergency-recovery
  - /enterprise/admin/articles/web-based-management-console
  - /enterprise/admin/categories/management-console
  - /enterprise/admin/articles/accessing-the-management-console
  - /enterprise/admin/guides/installation/web-based-management-console
  - /enterprise/admin/installation/accessing-the-management-console
  - /enterprise/admin/configuration/accessing-the-management-console
  - /admin/configuration/accessing-the-management-console
versions:
  ghes: '*'
type: how_to
topics:
  - Enterprise
  - Fundamentals
shortTitle: Access the management console
---
## About the {% data variables.enterprise.management_console %}

Use the {% data variables.enterprise.management_console %} for basic administrative activities:
- **Initial setup**: Walk through the initial setup process when first launching {% data variables.location.product_location %} by visiting {% data variables.location.product_location %}'s IP address in your browser.
- **Configuring basic settings for your instance**: Configure DNS, hostname, SSL, user authentication, email, monitoring services, and log forwarding on the Settings page.
- **Scheduling maintenance windows**: Take {% data variables.location.product_location %} offline while performing maintenance using the {% data variables.enterprise.management_console %} or administrative shell.
- **Troubleshooting**: Generate a support bundle or view high level diagnostic information.
- **License management**: View or update your {% data variables.product.prodname_enterprise %} license.

You can always reach the {% data variables.enterprise.management_console %} using {% data variables.location.product_location %}'s IP address, even when the instance is in maintenance mode, or there is a critical application failure or hostname or SSL misconfiguration.

To access the {% data variables.enterprise.management_console %}, you must use the administrator password established during initial setup of {% data variables.location.product_location %}. You must also be able to connect to the virtual machine host on port 8443. If you're having trouble reaching the {% data variables.enterprise.management_console %}, please check intermediate firewall and security group configurations.

The {% data variables.enterprise.management_console %} password hash is stored in `/data/user/common/secrets.conf`, and that file is automatically synced from the primary appliance to any high-availability replicas. Any change to the primary's password will automatically be replicated to high-availability replicas. For more information about high availability, see "[About high availability configuration](/admin/enterprise-management/configuring-high-availability/about-high-availability-configuration)."

## Accessing the {% data variables.enterprise.management_console %} as a site administrator

The first time that you access the {% data variables.enterprise.management_console %} as a site administrator, you must upload your {% data variables.product.prodname_enterprise %} license file to authenticate into the app. For more information, see "[Managing your license for {% data variables.product.prodname_enterprise %}](/billing/managing-your-license-for-github-enterprise)."

{% data reusables.enterprise_site_admin_settings.access-settings %}
{% data reusables.enterprise_site_admin_settings.management-console %}
{% data reusables.enterprise_management_console.type-management-console-password %}

## Accessing the {% data variables.enterprise.management_console %} as an unauthenticated user

1. Visit this URL in your browser, replacing `hostname` with your actual {% data variables.product.prodname_ghe_server %} hostname or IP address:
  ```shell
  http(s)://HOSTNAME/setup
  ```
{% data reusables.enterprise_management_console.type-management-console-password %}

## Unlocking the {% data variables.enterprise.management_console %} after failed login attempts

The {% data variables.enterprise.management_console %} locks after ten failed login attempts are made in the span of ten minutes. You must wait for the login screen to automatically unlock before attempting to log in again. The login screen automatically unlocks as soon as the previous ten minute period contains fewer than ten failed login attempts. The counter resets after a successful login occurs.

To immediately unlock the {% data variables.enterprise.management_console %}, use the `ghe-reactivate-admin-login` command via the administrative shell. For more information, see "[Command line utilities](/enterprise/admin/guides/installation/command-line-utilities#ghe-reactivate-admin-login)" and "[Accessing the administrative shell (SSH)](/enterprise/admin/guides/installation/accessing-the-administrative-shell-ssh/)."

## Troubleshooting failed connections to the {% data variables.enterprise.management_console %}

If you cannot connect to the {% data variables.enterprise.management_console %} on {% data variables.location.product_location %}, you can review the following information to troubleshoot the problem.

### Error: "Your session has expired" for connections through a load balancer

If you access {% data variables.location.product_location %} through a load balancer and connections to the {% data variables.enterprise.management_console %} fail with a message that your session has expired, you may need to reconfigure your load balancer. For more information, see "[Using {% data variables.product.product_name %} with a load balancer](/admin/configuration/configuring-network-settings/using-github-enterprise-server-with-a-load-balancer#error-your-session-has-expired-for-connections-to-the-management-console)."
