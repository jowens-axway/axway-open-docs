---
title: API Portal 7.7 November 2020 Release Notes
linkTitle: API Portal November 2020
weight: 60
date: 2020-11-05
---
## Summary

API Portal provides an API consumer-facing interface that you can customize to match your corporate brand. API Portal is a layered product linked to API Manager, and requires both API Manager and API Gateway. For more information, see the API Gateway and API Manager documentation.

## Installation

API Portal is available as a software installation or a virtualized deployment in a Docker container. For more information, see the following options:

* If you are installing API Portal for the first time using this update, see [Install API Portal](/docs/apim_installation/apiportal_install/)
* If you are already using API Portal (7.5.x, 7.6.x, 7.7.x) and want to install this update, see [Upgrade API Portal](/docs/apim_installation/apiportal_install/upgrade_automatic/)
* If you want to deploy API Portal in Docker containers, see [Deploy API Portal in containers](/docs/apim_installation/apiportal_docker/)

## New features and enhancements

### Production Ready Docker Container - Phase 1

* Internal security review completed.
* CentOS8 supported.
* Build and run docker as non-root user.
* This is release 1 of the production ready docker container.

  * From release 1 onwards the container will be upgradable.
  * No upgrade is supported from any previous docker containers of the API Portal.

### Red Hat Enterprise 8 Support

* Official support added for RHEL 8 for the standalone (non-docker) API Portal.
* Supported [platform matrix](https://docs.axway.com/bundle/Axway_Products_SupportedPlatforms_allOS_en/resource/Axway_Products_SupportedPlatforms_allOS_en.pdf) updated to include RHEL8.

### Security

* Virus scanning of uploaded files via the Portal interface.

### Upgrade Script Updates

* In July 2020, we released a "cumulative" upgrade script, `apiportal_cumulative_upgrade.sh`to help customers transition from 7.5.5 / 7.6 up to 7.7 July 2020​ update.
* This script has been updated to upgrade customers to the 7.7 November 2020 update inline with the end of support for the 7.5.x and 7.6.x product lines​ in November 2020.
* For more information, see [Upgrade API Portal using the cumulative upgrade script](/docs/apim_installation/apiportal_install/upgrade_automatic/#upgrade-api-portal-using-the-cumulative-upgrade-script).

### User Experience Improvements

* Sort API catalog by Newest/Oldest APIs​ in the API Catalog
* Configuration setting in the Joomla Admin interface to show/hide APIs in the catalog by status

## Limitations of this update

This update has the following limitations:

* API Portal 7.7.20201130 is compatible with API Gateway and API Manager 7.7.20201130 only.
* Upgrade to API Portal 7.7.20201130 is supported from [API Portal 7.7](/docs/apim_relnotes/201904_release/apip_relnotes/) only. You can use the [cumulative upgrade script](/docs/apim_installation/apiportal_install/upgrade_automatic/#upgrade-api-portal-using-the-cumulative-upgrade-script) to upgrade directly from earlier versions (for example, 7.5.5, 7.6.2) to API Portal 7.7 November, or see [API Portal single version upgrade](/docs/apim_installation/apiportal_install/upgrade_automatic/#upgrade-from-api-portal-7-6-2) to upgrade versions incrementally.
* Upgrading from previous API Portal Docker image is not supported.
* This update is not available as a virtual appliance or as a managed service on Axway Cloud.

## Important changes

It is important, especially when upgrading from an earlier version, to be aware of the following changes in the behavior or operation of the product in this update.

## Deprecated features

<!-- Add features that are deprecated here -->

As part of our software development life cycle we constantly review our API Management offering. As part of this review, no capabilities have been deprecated.

## Removed features

### Enable user listing configuration

After a recent security fix in API Manager, the **Enable user listing** option is no longer needed in API Portal, and has been removed.

For previous versions of API Portal, which still use the **Enable user listing** option, see [API Portal - Customize application sharing settings](https://support.axway.com/en/admin/kbadmin/article-details/id/181283).

Related Issues: IAP-3616, RDAPI-17343

## Fixed issues

This version of API Portal includes:

* Fixes from all 7.5.5, 7.6.2, and 7.7 service packs released prior to this version. For details of all the service pack fixes included, see the corresponding *SP Readme* attached to each service pack on [Axway Support](https://support.axway.com).
* Fixes from all 7.7 updates released prior to this version. For details of all the update fixes included, see the corresponding [release note](/docs/apim_relnotes/) for each 7.7 update.

### Fixed security vulnerabilities

| Internal ID | Case ID | CVE Identifier | Description                                                                                                                                                                                                                                                                                                    |
| ----------- | ------- | -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IAP-3180    |         |                | **Issue**: PII (Personally identifiable information) appearing in log files. **Resolution**: PII such as user name is replaced with associated GUID in log files.                                                                                                                                              |
| IAP-3179    |         |                | **Issue**: Insufficient logging for successful logins, access control failures, failed input validation attempts. **Resolution**: Now each log entry includes the necessary information that would help in a detailed investigation of the timeline when an event has happened.                                |
| IAP-3579    | 1195741 |                | **Issue**: XSS was possible on TryIt page. **Resolution**: The \`apiId\` query param is now sanitized before outputted.                                                                                                                                                                                        |
| IAP-3175    |         |                | **Issue**: When SSO is configured, log information coming from untrusted sources is not sanitized in any way, making it possible for an attacker to inject new lines in the logs. **Resolution**: The data now is sanitized.                                                                                   |
| IAP-3652    | 1195741 |                | **Issue**: HTTP Host header can be controlled by an attacker. **Resolution**: Documentation was update whith information on how to prevent this. For more information, see [Prevent host header attack](/docs/apim_installation/apiportal_install/secure_harden_portal/index.html#prevent-host-header-attack). |
| IAP-3178    |         |                | **Issue**: Passwords containing leading or trailing spaces were trimmed. **Resolution**: Leading or trailing spaces are considered as legitimate characters in password.                                                                                                                                       |

### Other fixed issues

| Internal ID | Case ID | Description                                                                                                                                                                             |
| ----------- | ------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| IAP-3559    | 1190447 | **Issue**: Generated authentications do not appear when Applications page is disabled. **Resolution**: Generated authentications are now displayed regardless Applications page status. |
| IAP-3564    | 1190447 | **Issue**: 'Create Application' button remains on Try-It page even when it is disabled in JAI. **Resolution**: JAI config option is taken into account.                                 |
| IAP-3730    | 1207734 | **Issue**: SQL query that is supposed to run only on upgrade, was also executed on installation. **Resolution**: The query is now executed only on upgrade.                             |

## Known issues

The following are known issues for this update.

### When Multi Manager feature is configured, API Portal users are no longer able to login

After a recent bug fix in API Manager (RDAPI-20021), the `Authenticate to Master` policy is no longer working in releases earlier than [API Portal July 2020](/docs/apim_relnotes/20200730_apip_relnotes/). To fix this, perform the following steps:

1. Open all slave managers configurations in Policy Studio, and click to **Edit** the `AuthenticateToMaster` policy.
2. Click the **Login to Master** (Connect to URL) filter, and enter `Accept: */*` for the **Request Protocol Header**.
3. Click the **Enter** key twice to create two blank lines after `Accept: */*`.

Related Issue:IAP-3435

### Page layout and alignment for Arabic language

Changing the API Portal language to Arabic (or any other right to left language) results in issues with page layout and alignment on the API Portal Home and Pricing pages, and some buttons are not visible. As a workaround, you can turn on the development mode in JAI. Follow these steps:

1. Log in to Joomla! Admin Interface (JAI).
2. In the JAI top navigation bar, click **Extensions > Templates**.
3. Click your template style (for example, `purity_III * Default`) to open it.
4. Click the **General** tab.
5. Change **Development Mode** to `ON`.
6. Click **Save** and click **Close** to close the template style.

Related Issue: IAP-308

## Documentation

This section describes documentation enhancements and related documentation.

### Documentation enhancements

The latest version of API Gateway, API Manager, and API Portal documentation has been migrated to Markdown format and is available in a [public GitHub repository](https://github.com/Axway/axway-open-docs) to prepare for future collaboration using an open source model. As part of this migration, the documentation has been restructured to help users navigate the content and find the information they are looking for more easily.

Documentation change history is now stored in GitHub. To see details of changes on any page, click the link in the **Last modified** section at the bottom of the page.

### Related documentation

To find all available documentation for this product version:

1. Go to [Manuals on the Axway Documentation portal](https://docs.axway.com/bundle).
2. In the left pane Filters list, select your product or product version.

Customers with active support contracts need to log in to access restricted content.

The following reference documents are also available:

* [Supported Platforms](https://docs.axway.com/bundle/Axway_Products_SupportedPlatforms_allOS_en) - Lists the different operating systems, databases, browsers, and thick client platforms supported by each Axway product.
* [Interoperability Matrix](https://docs.axway.com/bundle/Axway_Products_InteroperabilityMatrix_allOS_en) - Provides product version and interoperability information for Axway products.

## Support services

The Axway Global Support team provides worldwide 24 x 7 support for customers with active support agreements.

Email [support@axway.com](mailto:support@axway.com) or visit [Axway Support](https://support.axway.com/).

See [Get help with API Gateway](/docs/apim_administration/apigtw_admin/trblshoot_get_help/) for the information that you should be prepared to provide when you contact Axway Support.