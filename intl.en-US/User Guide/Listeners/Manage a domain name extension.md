# Manage a domain name extension {#concept_blk_jy1_wdb .concept}

HTTPS listeners of guaranteed-performance SLB support configuring multiple certificates, allowing you to forward requests with different domain names to different backend servers.

## Introduction to SNI {#section_kfl_lsc_wdb .section}

Server Name Indication \(SNI\) is an extension to the SSL/TLS protocol, allowing a server to install multiple SSL certificates on the same IP address. When a client accesses SLB, the certificate configured for the domain name is used by default. If no certificate is configured for the domain name, the certificate configured for the HTTPS listener is used.

**Note:** Only guaranteed-performance SLB instances support SNI.

If you want to resolve multiple domain names to the IP address of an SLB instance, and distribute requests with different domain names to different backend servers, use the domain name extension function.

The domain name extension function is available in all regions.

## Add a domain name extension {#section_ykj_pvb_wdb .section}

1.  Log on to the [SLB console](https://partners-intl.aliyun.com/login-required#/slb).
2.  Select a region and all SLB instance in this region are displayed.
3.  Click the ID of the SLB instance.
4.  In the left-side navigation pane, click **Listeners**.
5.  On the Listeners page, find the created HTTPS listener, and then click **More** \> **Additional Domains**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15661/15421809857466_en-US.png)

6.  Click **Add Additional Domain** and configure the domain name:
    1.  Enter a domain name. The domain can only contain letters, numbers, dashes, or dots.

        Domain forwarding rules support exact match and wildcard match.

        -   Exact domain name: www.aliyun.com
        -   Wildcard domain name \(generic domain name\): \*.aliyun.com, \*.market.aliyun.com

            When a request matches multiple forwarding rules, exact match takes precedence over small-scale wildcard match and small-scale wildcard match takes precedence over large-scale wildcard match, as shown in the following table.

            |Type|Request URL|Domain name based forwarding rule|
|www.aliyun.com|\*.aliyun.com|\*.market.aliyun.com|
            |:---|:----------|:--------------------------------|
            |:-------------|:------------|:-------------------|
            |Exact match|www.aliyun.com|✓|×|×|
            |Wildcard match|Market.aliyun.com|×|✓|×|
            |Wildcard match|info.market.aliyun.com|×|×|✓|

    2.  Select the certificate associated with the domain name.

        **Note:** The domain name in the certificate must be the same as the added domain name extension.

    3.  Click **OK**.

        ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15661/15421809857467_en-US.png)

7.  On the Listeners page, find the created HTTPS listener and click **Add Forwarding Rules**.
8.  On the Forwarding Rules page, click **Add Forwarding Rules**.
9.  For more information, see [Add domain-name based or URL-based forwarding rules](reseller.en-US/Tutorials/Traffic forwarding based on domain name or URL.md#).

    **Note:** Make sure that the domain name configured in the forwarding rule is the same as the added domain name extension.


## Edit a domain name extension {#section_fns_2qc_wdb .section}

You can replace the certificate used by an added domain name extension.

To edit a domain name extension, complete these steps:

1.  Log on to the [SLB console](https://partners-intl.aliyun.com/login-required#/slb).
2.  Select a region and all SLB instances in this region are displayed.
3.  Click the ID of the SLB instance.
4.  In the left-side navigation pane, click **Listeners**.
5.  On the Listeners page, find the created HTTPS listener, and then click **More** \> **Additional Domains**.
6.  Find the target domain name extension and then click **Edit**.
7.  In the Edit Additional Domain dialog box, select a new certificate and then click **OK**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15661/15421809857468_en-US.png)


## Delete a domain name extension {#section_htc_j1p_42b .section}

To delete a domain name extension, complete these steps:

1.  Log on to the [SLB console](https://partners-intl.aliyun.com/login-required#/slb).
2.  Select a region and all SLB instance in this region are displayed.
3.  Click the ID of the SLB instance.
4.  In the left-side navigation pane, click **Listeners**.
5.  On the Listeners page, find the created HTTPS listener, and then click **More** \> **Additional Domains**.
6.  Find the target domain name extension and then click **Delete**.

    ![](http://static-aliyun-doc.oss-cn-hangzhou.aliyuncs.com/assets/img/15661/15421809867469_en-US.png)

7.  In the displayed dialog box, click **OK**.

