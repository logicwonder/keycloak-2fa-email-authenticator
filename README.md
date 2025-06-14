# 🔒 Keycloak 2FA Email Authenticator

Keycloak Authentication Provider implementation to get a two factor authentication with an OTP (One-time-password) send via Email (through SMTP).

When logging in with this provider, you can send a verification code (OTP) to the user's e-mail address.
Tested with Keycloak version 26.x. If you are using a different Keycloak version, don't forget to change the version in pom.xml file.

The [Server Development part of the Keycloak reference documentation](https://www.keycloak.org/docs/latest/server_development/index.html) contains additional resources and examples for developing custom Keycloak extensions.

# Development

If you are using Eclipse, you need to install the Lombok plugin, otherwise Eclipse cannot resolve `log` which is declared at runtim through @JBossLog annotation.
Find further information at https://projectlombok.org/setup/eclipse


# 🚀 Deployment

## Artifact

You can download the necessary artifacts for Keycloak 2FA Email Authenticator from the [release on GitHub.](https://github.com/mesutpiskin/keycloak-2fa-email-authenticator/releases/tag/v0.4) Please choose the appropriate version based on your Keycloak installation.

## Providers

`mvn package` will create a jar file.
copy `keycloak-2fa-email-authenticator.jar` to `keycloak/providers/` directory.

If you are Dockerized keycloak then copy to `/opt/jboss/keycloak/standalone/deployments/` directory.

## Build

Don't forget to start kc.sh with build parameter to make KeyCloak recognize the new povider:

> bin/kc.sh build

# Configuration

## Email Configuration

Don't forget to configure your realm's SMTP settings, otherwise no email will be send:
1. Login as admin on your KeyCloak installation.
2. Switch to your realm
3. Click `Realm settings` from the menu on the left.
4. Click on the `Email`-tab and enter your smpt data.

## Theme configuration

Copy the themes/keycloak.v2.extended folder to keycloak/themes folder to render the Email Authenticator in the authenticator selector UI.

## Authentication Flow
Create new browser login authentication flow and add Email OTP flow after Username Password Form.
Set the requirement for Email OTP flow to Alternate to make it work along with existing 2FA (either or)
<img src="static/otp-form.png">
