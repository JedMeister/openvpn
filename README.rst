VPN solution built with OpenVPN® Community Edition - Open Source VPN
====================================================================

`OpenVPN®`_ Community Edition provides a full-featured open source SSL/TLS
Virtual Private Network (VPN). The TurnKey Linux VPN software appliance
leverages the open source 'openvpn-server', 'openvpn-client' and 'easy-rsa'
software (developed by OpenVPN® Inc.) to support "site-to-site" or "gateway"
access. "Site-to-site" can link 2 otherwise unconnected LANs; suitable for
multi-site enterprise networks or linkage to an Amazon VPC. "Gateway"
configuration can secure traffic across public and/or insecure wifi
connections and/or provide a secure solution for remote work scenarios.

This appliance includes all the standard features in `TurnKey Core`_,
and on top of that:

- OpenVPN® configurations:

    - Initialization hooks to configure common OpenVPN® deployments
      such as "site-to-site" server or client and gateway profiles.
    - All profiles support SSL/TLS certificates for authentication and
      key exchange.
    - Server and gateway deployments include a convenience script to add
      clients, generating all required keys and certificates, as well as
      a unified ovpn profile for clients to easily connect to the VPN.
    - Expiring obfuscated HTTPS urls can be created for clients to
      download their profiles (especially useful with mobile devices
      using a QR code scanner).
    - The server profile supports a private subnet configuration,
      enabling clients to reach servers behind the OpenVPN® server.
    - The gateway profile configures connecting clients to tunnel all
      their traffic through the VPN.
    - When adding clients in a server or gateway deployment, an optional
      parameter can be given to enable computers on a subnet behind the
      client to connect to the VPN.
    - For added security, OpenVPN® is configured to drop privilages,
      run in a chroot jail dedicated to CRL, and uses tls-auth for HMAC
      signature verification protecting againsts DoS attacks, port
      flooding, port scanning and buffer overflow vulnerabilities in the
      SSL/TLS implementation.

See the `Usage documentation`_ for further details, including Amazon VPC
notes and cloudformation template.

**Note**: OpenVPN® is a registered trademark of OpenVPN® Inc. Neither
TurnKey Linux nor this software appliance are affiliated with or endorsed
by OpenVPN® Inc.

Potential issues caused by timezone mismatch
--------------------------------------------

Some VPN client applications expect certificate timestamps to be in local
time. However, by default, TurnKey servers use UTC time.

That can lead to the creation of certificates, which according to local
time, are not yet valid. Under these circumstance, connection will fail.

To avoid that, please set the timezone for your TurnKey OpenVPN server
prior to further configuration. To do that via the commandline::

    dpkg-reconfigure tzdata

For further info re setting timezone, please see this_ TurnKey Blog post.

Credentials *(passwords set at first boot)*
-------------------------------------------

-  Webmin, SSH: username **root**

.. _OpenVPN®: https://openvpn.net
.. _TurnKey Core: https://www.turnkeylinux.org/core
.. _Usage documentation: https://github.com/turnkeylinux-apps/openvpn/tree/master/docs
.. _this: https://www.turnkeylinux.org/blog/configuring-timezone
