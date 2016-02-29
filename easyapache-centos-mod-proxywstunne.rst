EasyApache mod_proxy_wstunnel
#############################

Install ``mode_proxy_wstunnel`` on EasyApache.

System
------

-  CentOs 6.7 (64 bit)
-  cPanel/WHM with EasyApache4
-  *root* ssh access

Resources
---------

-  https://features.cpanel.net/topic/add-mod\_proxy\_wstunnel-to-easyapache
-  https://documentation.cpanel.net/display/EA4/EasyApache+4+%28EA4%29+-+How-To's
-  https://httpd.apache.org/docs/2.4/mod/mod\_proxy\_wstunnel.html
-  An EasyApache 3 option using Apache Extension tools *apxs*
   https://forums.cpanel.net/threads/limiting-bandwidth-per-ip.136477/#post586877

General Steps
-------------

-  Switch to EasyApache 4 if the system is running EasyApache 3
   ``/scripts/migrate_ea3_to_ea4 --run``
-  Create new profile by copying a file from
   ``/etc/cpanel/ea4/profiles/cpanel`` to
   ``/etc/cpanel/ea4/profiles/cpanel`` (Check `example profile in
   files <http://dev-server/open-source/opensourcewiki/blob/master/allphp-proxy_ws.json>`__)
-  Install the new profile
   ``ea_install_profile </full/path/to/profile.json> --install``
-  From ``WHM``, choose *EasyApache 4* settings, and Select
   **Provision** for the correct profile.
-  Wait until Easy Apache configure the profile and review the logs
   after the profile is provisioned.

