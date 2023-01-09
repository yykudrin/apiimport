# SodaApiV2

## Background

The SodaApiV2 was initially developed in 7 weeks time by two developers. Unfortunately there were no
written requirements at the time of development.

We used the ApiV1 and problems we had previously identified with that version to improve
the API and implement the necessary features.

Due to problems with the database model, we also implemented some workarounds (mainly due to inconsistencies
in the DB design and enforced constraints, etc.).

Due to budget constraints there was neither time nor budged allocated to tests / test coverage.

## Installation

### Prequisites

* **JDK 11** (open JDK or any other standard-compliant vendor Java SDK),
* Firewall connectivity to communicate with
  * Kafka,
  * Database.
* `secret` folder was created relative to the jar file (same folder).

### Build the jar file

_Note: If you have received a prebuilt JAR file, you can skip this section._

To build the JAR file, execute the command

`mvn clean install`

This will result in an UBER-jar being created under App/target.
The name of the target jar file is `ApiV2.jar`.

### Run the JAR file with JDK 11

#### Public Mode (e.g. used by https://www.picture-alliance.com)

The public mode requires a few different (and additional settings) because if the application
is deployed as admin backend used by the admin frontend, the application provides less features than
when run in public mode.

#### Admin Mode (e.g. used by https://admin.picture-alliance.com)

The admin mode does not require some settings the public mode is using. The admin mode instance is
deployed as backend for the admin frontend. 

#### Edit the .env file

**Please copy the file `env-sample` to `.env` and edit the configuration accordingly.**

<table>
    <tr><th>Parameter Name</th><th>Used for admin instance?</th><th>Description</th><th>Example</th><th>Done</th></tr>
    <tr><td>SODAENV</td><td>Yes</td><td>Environment to use. This impacts what integrated configuration file will be used by the application. Possible values: local, stage, prod, admin-stage, admin-prod</td><td>stage</td><td>&#10003;</td></tr>
    <tr><td>APP_SODA_SYSTEM_UID</td><td>Yes</td><td>Environment/project ID to use. This must match the DB instance (db_1078 would be 1078).</td><td>1100</td><td>&#10003;</td></tr>
    <tr><td>SPRING_DATASOURCE_URL</td><td>Yes</td><td>JDBC URL of the database to use.</td><td>jdbc:mysql://localhost:3308/db_1078?serverTimezone=UTC&zeroDateTimeBehavior=convertToNull&charset=UTF8</td><td>&#10003;</td></tr>
    <tr><td>SPRING_DATASOURCE_USERNAME</td><td>Yes</td><td>Username of the database user.</td><td>SodaApiUser</td><td>&#10003;</td></tr>
    <tr><td>SPRING_DATASOURCE_PASSWORD</td><td>Yes</td><td>Password of the database user.</td><td>SomeWeirdPassword@@19091028!098 (not valid!)</td><td>&#10003;</td></tr>
    <tr><td>SPRING_MAIL_HOST</td><td>Yes</td><td>Mail Server</td><td>email-smtp.eu-central-1.amazonaws.com</td><td>&#10003;</td></tr>
    <tr><td>SPRING_MAIL_USERNAME</td><td>Yes</td><td>Mail user</td><td>AKIAA5B22AZCKI112A12 (not valid!)</td><td>&#10003;</td></tr>
    <tr><td>SPRING_MAIL_PASSWORD</td><td>Yes</td><td>Mail user's password</td><td>SomeWeirdPassword@!@!89291825 (not valid!)</td><td>&#10003;</td></tr>
    <tr><td>SPRING_KAFKA_BOOTSTRAP_SERVERS</td><td>No</td><td>Comma-separated URLs of KAFKA bootstrap servers.</td><td>localhost:9092</td><td>&#10003;</td></tr>
    <tr><td>SECURITY_TOKEN_ISSUER</td><td>Yes</td><td>Issuer of the JWT token.</td><td>https://apiv2.pa.sodatech.com</td><td>&#10003;</td></tr>
    <tr><td>SECURITY_COOKIE_CONFIGURED_DOMAIN</td><td>Yes</td><td>Issuer of the JWT token (for cookie mode).</td><td>apiv2.pa.sodatech.com</td><td>&#10003;</td></tr>
    <tr><td>SECURITY_SSO_ENABLED</td><td>No</td><td>Is DPA single sign-on enabled on this instance? This will only be enabled on the public instance. Disable for admin environment.</td><td>true</td><td>&#10003;</td></tr>
    <tr><td>SECURITY_SSO_KEYRETRIEVALURL</td><td>No</td><td>URL where to fetch the DPA SSO public key.</td><td>https://keys.dpa-connect.de/v1/key/sso.dpa-id.de</td><td>&#10003;</td></tr>
    <tr><td>APP_AWS_CLOUDFRONT_KEYPAIRID</td><td>Yes</td><td>Key Pair ID of your cloudfront distribution's Key Pair.</td><td>APSJKSFJKSJFKJII2kjlk3Q (not valid!)</td><td>&#10003;</td></tr>
    <tr><td>APP_AWS_CLOUDFRONT_DOWNLOADBASE_URL</td><td>Yes</td><td>Key Pair ID of your cloudfront distribution's Key Pair.</td><td>https://img.pa-test.sodatech.com</td><td>&#10003;</td></tr>
    <tr><td>APP_AWS_AWS_ACCESSKEY</td><td>Yes</td><td>AWS Lambda Access Key. Used to access AWS lambda functions.</td><td>AKIAA5B22AZCKI112A12 (not valid!)</td><td>&#10003;</td></tr>
    <tr><td>APP_AWS_AWS_SECRETKEY</td><td>Yes</td><td>AWS Lambda Secret Key. Used to access AWS lambda functions.</td><td>ab3klLaMA2LABB/klMmNAAc+LYNNAakajswjDe11 (not valid!)</td><td>&#10003;</td></tr>
    <tr><td>APP_AWS_S3_ACCESSKEY</td><td>Yes</td><td>AWS S3 Access Key</td><td>AKIAA5B22AZCKI112A12 (not valid!)</td><td>&#10003;</td></tr>
    <tr><td>APP_AWS_S3_SECRETKEY</td><td>Yes</td><td>AWS S3 Secret Key</td><td>ab3klLaMA2LABB/klMmNAAc+LYNNAakajswjDe11 (not valid!)</td><td>&#10003;</td></tr>
    <tr><td>APP_SECURITY_GOOGLE_RECAPTCHA_SECRETKEY</td><td>No</td><td>Google Recaptcha (V2) Secret Key</td><td>6LeaKsjAJ2jsFkaKL2jkFk21AK2jFGj2J2jJlasm (not valid!)</td><td>&#10003;</td></tr>
    <tr><td>APP_PDF_ASSET_DOWNLOAD_URL</td><td>Yes</td><td>URL to download PDF assets (Asset's PDF file)</td><td>https://img.pa-test.sodatech.com/go/Asset/downloadPdf/{ASSET_ID}?lang={LANG}</td><td>&#10003;</td></tr>
    <tr><td>APP_MEDIA_DELETED_ASSET_PLACEHOLDER_URL</td><td>Yes</td><td>URL of the image displayed when an asset was deleted.</td><td>https://img.pa-test.sodatech.com/public/asset-deleted.jpg</td><td>&#10003;</td></tr>
    <tr><td>APP_MEDIA_DELETED_ASSET_PLACEHOLDER_HEIGHT</td><td>Yes</td><td>Height of the deleted asset placeholder image.</td><td>1134</td><td>&#10003;</td></tr>
    <tr><td>APP_MEDIA_DELETED_ASSET_PLACEHOLDER_WIDTH</td><td>Yes</td><td>WIDTH of the deleted asset placeholder image.</td><td>852</td><td>&#10003;</td></tr>
    <tr><td>APP_FRONTEND_REGISTRATION_PAGE_URL</td><td>Yes - startup only</td><td>URL of the frontend registration page used for DPA registration.</td><td>http://localhost:4200/dpa-id-callback/?type=register</td><td>&#10003;</td></tr>
    <tr><td>APP_FRONTEND_INVALID_TOKEN_PAGE_URL</td><td>Yes - startup only</td><td>URL of the page to display when a DPA ID user is using an invalid (SSO) JWT.</td><td>http://localhost:4200/dpa-id-callback/?type=error</td><td>&#10003;</td></tr>
    <tr><td>APP_FRONTEND_LANDING_PAGE_URL</td><td>Yes - startup only</td><td>URL of the landing page after successfully registering a DPA SSO user.</td><td>http://localhost:4200/dpa-id-callback/?type=success</td><td>&#10003;</td></tr>
    <tr><td>APP_FRONTEND_DEACTIVATED_ACCOUNT_PAGE_URL</td><td>Yes - startup only</td><td>URL of the page a deactivated DPA ID SSO user is redirected to.</td></td><td>http://localhost:4200/dpa-id-callback/?type=error\&status=deactivated</td><td>&#10003;</td></tr>
    <tr><td>APP_FRONTEND_ALLOWED_REDIRECT_HOSTS</td><td>Yes - startup only</td><td>List of base-URIs to which we are allowed to redirect users. The frontend will pass a URL to which we are supposed to redirect a user. For security reasons, the URL has to start with this URI.</td><td>https://next.picture-alliance.com/, http://localhost:4200/, http://stage.picture-alliance.com/</td><td>&#10003;</td></tr>
    <tr><td>APP_ROUTE_FRONTEND_BASE_URL</td><td>Yes</td><td>URL link to access a lightbox using a token. Used when sending an email to share a lightbox.</td><td>https://localhost:4200/lightbox/token/</td><td>&#10003;</td></tr>
</table>

##### Secret folder

Please create a folder with the name `secret` in your working directory.

The secret directory should contain the following files:

* `cloudfront_private_key.der`,
* `private_key.der`.

<table>
    <tr><th>Filename</th><th>Description</th></tr>
    <tr><td><i>cloudfront_private_key.der</i></td><td>Private key of your cloudfront distribution (i.e. the distribution that will serve files!)</td></tr>
    <tr><td><i>private_key.der</i></td><td>Custom private key of cert used to create the signatures for the JSON Web Token.</td></tr>
</table>

`private_key.der` can simply be created with openssl (RS256).

##### Running the application

You can execute the application file using the following command:

`run.sh`

This simply sources the `.env` file and starts the application.

# Context Paths

The context path for ApiV2 in public mode is `/api`.

The context path for ApiV2 in admin mode is `/adminapi`.
