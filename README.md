# Welcome to the hosting partners program!

In this directory, you'll find information on provisioning and managing plans for Automattic products as well as information on managing the products themselves.

If you have any technical questions or concerns, don’t hesitate to get in touch with our team via Slack or by emailing us at `partners@jetpack.com`.

## Documentation links

- Jetpack
  - [Jetpack Licensing API](https://github.com/Automattic/jetpack-licensing-api)
  - [Jetpack Coupons API](https://github.com/Automattic/jetpack-partner-api/tree/master/coupon)
  - Jetpack Start API:
      - [Authentication](jetpack/jetpack-start-endpoints/authentication.md)
      - Plan provisioning
        - ~~[Via CLI](jetpack/plan-provisioning.md)~~ (deprecated)
        - [Via direct API call](jetpack/jetpack-start-endpoints/plan-provisioning.md)
      - Checking status
        - [Connection status](jetpack/determining-connection-status.md)
        - [Provisioning status](jetpack/jetpack-start-endpoints/determining-provisioning-status-v1.4.md)
      - [Plan cancellation](jetpack/jetpack-start-endpoints/plan-cancellation.md)
      - [Controlling the redirect after a user finishes connection authorization](jetpack/redirect-after-authorization.md)
      - [Upgrade paths](jetpack/jetpack-start-endpoints/upgrade-paths.md)
      - [Managing modules](jetpack/managing-modules.md)
      - [Upgrade redirection](jetpack/upgrade-redirection.md)
      - [Monitor downtime notifications webhook](jetpack/monitor-downtime-notifications-webhook.md)
      - [Magic mobile links](jetpack/jetpack-start-endpoints/mobile-magic-link.md)
      - [Setting Backups SSH credentials](jetpack/jetpack-start-endpoints/setting-backups-ssh-credentials.md)
      - [Setting Backups FTP credentials](jetpack/jetpack-start-endpoints/setting-backups-ftp-credentials.md)
      - [Errors](jetpack/jetpack-start-endpoints/errors.md)
      - Activity, Backup, and Scan
        - [Fetch Activities](jetpack/jetpack-activity-endpoints/activity.md)
        - [Activity Group Counts](jetpack/jetpack-activity-endpoints/activity-count.md)
        - [Queue Restore](jetpack/jetpack-restore-endpoints/restore.md)
        - [Restore Status](jetpack/jetpack-restore-endpoints/restore-status.md)
        - [Fetch Backups](jetpack/jetpack-backup-endpoints/backups.md)
        - [Prepare Download](jetpack/jetpack-backup-endpoints/prepare-download.md)
        - [Download Status](jetpack/jetpack-backup-endpoints/downloads.md)
- WooCommerce
  - [Overview](woocommerce/overview.md)
  - [Provison/Register plan](woocommerce/plan-register.md)
  - [Cancel plan](woocommerce/plan-cancel.md)
  - [Update URL for a site](woocommerce/update-url.md)
  - [Update site connected to a plan](woocommerce/update-connected-site.md)
  - [Install product](woocommerce/install.md)
  - [Product information](woocommerce/product-info.md)
  - [Management via WP-CLI](woocommerce/management-via-wp-cli.md)
- Account creation
  - [Creating users via /jpphp/user endpoint](users/user-creation.md)
  - [Automatic account creation via Jetpack](jetpack/automatic-account-creation-connection.md)

## Become a hosting partner

If you're not already a hosting partner, and you'd like some more information, head on over to [https://jetpack.com/for/hosts/](https://jetpack.com/for/hosts/) to get started!

## Change log

- 2025-02-26 Added pages for install and update-connected-site endpoints.
- 2020-04-27 Added change log. Added page for status endpoint v1.4.
