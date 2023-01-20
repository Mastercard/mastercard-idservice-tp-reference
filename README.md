# ID for Trust Providers Reference Implementation

[![](https://developer.mastercard.com/_/_/src/global/assets/svg/mcdev-logo-dark.svg)](https://developer.mastercard.com/)

[![](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](./LICENSE)
[![](https://sonarcloud.io/api/project_badges/measure?project=Mastercard_mastercard-idservice-tp-reference-app&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=Mastercard_mastercard-idservice-tp-reference-app)
[![](https://sonarcloud.io/api/project_badges/measure?project=Mastercard_mastercard-idservice-tp-reference-app&metric=coverage)](https://sonarcloud.io/summary/new_code?id=Mastercard_mastercard-idservice-tp-reference-app)
[![](https://sonarcloud.io/api/project_badges/measure?project=Mastercard_mastercard-idservice-tp-reference-app&metric=vulnerabilities)](https://sonarcloud.io/summary/new_code?id=Mastercard_mastercard-idservice-tp-reference-app)

## Table of Contents
- [Overview](#overview)
  * [References](#references)
- [Usage](#usage)
  * [Prerequisites](#prerequisites)
  * [Configuration](#configuration)
  * [Integrating with OpenAPI Generator](#integrating-with-openapi-generator)
  * [OpenAPI Generator Plugin Configuration](#openAPI_generator_plugin_configuration)
  * [Generating The API Client Sources](#generating_the_API_client_sources)
  * [Running the Project](#running-the-project)
  * [Use Cases](#use-cases)
- [API Reference](#api-reference)
  * [Request Examples](#request-examples)
- [Support](#support)

## Overview <a name="overview"></a>
ID for Trust Providers is a digital identity service from Mastercard that helps you apply for, enroll in, log in to, and access services more simply, securely and privately. Rather than manually providing your information when you are trying to complete tasks online or in apps, ID enables you to share your verified information automatically, more securely, and with your consent and control. ID also enables you to do away with passwords and protects your personal information. Please see here for more details on the API: [ID for Trust Providers](https://developer.mastercard.com/mastercard-id-for-tp/documentation/).

For more information regarding the program, refer to [ID Service](https://idservice.com/)

### References <a name="references"></a>
* [Mastercard's OAuth Signer library](https://github.com/Mastercard/oauth1-signer-java)
* [Using OAuth 1.0a to Access Mastercard APIs](https://developer.mastercard.com/platform/documentation/using-oauth-1a-to-access-mastercard-apis/)
* [Mastercard's Payload Encryption/Decryption library](https://github.com/Mastercard/client-encryption-java)
* [Using Payload Encryption](https://developer.mastercard.com/platform/documentation/security-and-authentication/securing-sensitive-data-using-payload-encryption/)

## Usage <a name="usage"></a>
### Prerequisites <a name="prerequisites"></a>
* [Mastercard Developers Account](https://developer.mastercard.com/dashboard) with access to ID for Trust Providers API.
* A text editor or IDE.
* [Spring Boot 2.2+ up to 2.7.x](https://spring.io/projects/spring-boot).
* [Apache Maven 3.3+](https://maven.apache.org/download.cgi).
* [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html).
* Set up the `JAVA_HOME` environment variable to match the location of your Java installation.

### Configuration <a name="configuration"></a>

1. Create an account at [Mastercard Developers](https://developer.mastercard.com/account/sign-up).
2. Create a new project and add `ID for Trust Providers` API to your project.
3. Download all the keys. It will download multiple files.
4. Select all `.p12` files, `.pem` file and copy it to `src/main/resources` in the project folder.
5. Open `${project.basedir}/src/main/resources/application.properties` and configure the parameters accordingly.

### Integrating with OpenAPI Generator <a name="integrating-with-openapi-generator"></a>
[OpenAPI Generator](https://github.com/OpenAPITools/openapi-generator) generates API client libraries from [OpenAPI Specs](https://github.com/OAI/OpenAPI-Specification).
It provides generators and library templates for supporting multiple languages and frameworks.

See also:
* [OpenAPI Generator (maven Plugin)](https://mvnrepository.com/artifact/org.openapitools/openapi-generator-maven-plugin)
* [OpenAPI Generator (executable)](https://mvnrepository.com/artifact/org.openapitools/openapi-generator-cli)
* [CONFIG OPTIONS for java](https://github.com/OpenAPITools/openapi-generator/blob/master/docs/generators/java.md)

#### OpenAPI Generator Plugin Configuration <a name="openAPI_generator_plugin_configuration"></a>
```xml
<!-- https://mvnrepository.com/artifact/org.openapitools/openapi-generator-maven-plugin -->
<plugin>
    <groupId>org.openapitools</groupId>
    <artifactId>openapi-generator-maven-plugin</artifactId>
    <version>${openapi-generator.version}</version>
    <executions>
        <execution>
            <goals>
                <goal>generate</goal>
            </goals>
            <configuration>
                <inputSpec>${project.basedir}/src/main/resources/mastercard-idservice-reference_api_spec.yaml</inputSpec>
                <generatorName>java</generatorName>
                <library>okhttp-gson</library>
                <generateApiTests>false</generateApiTests>
                <generateModelTests>false</generateModelTests>
                <configOptions>
                    <sourceFolder>src/gen/main/java</sourceFolder>
                    <dateLibrary>java8</dateLibrary>
                </configOptions>
            </configuration>
        </execution>
    </executions>
</plugin>
```

#### Generating The API Client Sources <a name="generating_the_API_client_sources"></a>
Now that you have all the required dependencies, you can generate the sources. To do this, use one of the following methods:

* **Using IDE**<br/>
  In IntelliJ IDEA (or any other IDE of your choice), open the Maven menu. Click the icons `Reimport All Maven Projects` and `Generate Sources and Update Folders for All Projects`.

* **Using Terminal or CMD**<br/>
  Navigate to the project's root directory within a terminal window and execute the `mvn clean compile` command.

### Running the Project <a name="running-the-project"></a>

* **VM Parameter for country selection**<br/>
  Pass VM Options for `userSelectedCountry`. `USA` set as default.<br/>
  Example: `-DuserSelectedCountry=BRA`

* **Using IDE**<br/>
  Navigate to the `com.mastercard.dis.mids.reference` package and right-click to run `MIDSReferenceApplication`

* **Using Terminal or CMD**<br/>
  Navigate to the project's root directory within a terminal window and execute the `mvn spring-boot:run` command.

* After that you can see all the menu options, such as:

1. Registering a User Profile
2. Access Token API (SDKToken)
3. Create User Identity
4. Multi-Access Token API (MultiSDKToken)
5. Access User Identity
6. Update ID Confirmations (Enrollment)
7. Update ID Confirmations (Re-authentication)
8. User Account Activity Searches
9. Email OTP
10. SMS OTP
11. User Profiles Identity Searches
12. Share User Identity (TP-TP)
13. RP Activity Searches
14. Audit Events
15. Delete ID
16. Share User Identity (TP-RP) (Enrollment)
17. Additional Document Support
18. Share User Identity (TP-RP) (Re-authentication)
19. TP Scopes
20. TP Data Shares
21. Update Identity
22. Create Watchlist Fraud Signal
23. Search for a Watchlist Fraud Signal
24. Delete Identity Attribute
25. Authentication Decisions
26. Exit

### Use cases <a name="use-cases"></a>
The main use cases in ID for Trust Providers Reference APIs are Personal Data Storage, SMS One Time Password, Email One Time Password, Document Verification, Multi Document Verification, Re-Authentication, GPA-Authentication, Claims Sharing, Audit Events, User Profile, Delete ID, TP Scopes Request and Fraud Data.

## API Reference <a name="api-reference"></a>

- To develop a client application that consumes the ID for Trust Providers API with Spring Boot, refer to the  [ID for Trust Providers Reference](https://developer.mastercard.com/mastercard-id-for-tp/documentation/api-reference/).

- The OpenAPI specification with `idservice` and `idwatchlist` endpoints can be found [here](https://developer.mastercard.com/mastercard-id-for-tp/documentation/reference-app/).

### Request Examples <a name="request-examples"></a>
You can change the default input passed to APIs, modify values in following file:
* `com.mastercard.dis.mids.reference.constants.Constants`

## Support <a name="support"></a>

- For further information, send an e-mail to `ID.Network.Support@mastercard.com`.
- For information regarding licensing, refer to the [LICENSE](LICENSE.md).
- For copyright information, refer to the [COPYRIGHT](COPYRIGHT.md).
- For instructions on how to contribute to this project, refer to the [CONTRIBUTING](CONTRIBUTING.md).
- For changelog information, refer to the [CHANGELOG](CHANGELOG.md).
