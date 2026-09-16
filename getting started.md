Top_of_page The Medidata Platform provides API resources so that you can create, analyze, plan, and implement clinical trial projects and retrieve their results. You can interact with Medidata resources from any system that sends HTTP requests.

There are many things you can do with the REST API. For example:

- An application can show data from Medidata on a website or in an application.
- You can upload large amounts of data that will later be consumed in your app.
- You can download recent data to update information in Medidata apps.
- Applications written in any programming language can interact with data on Medidata.

In this site, find the information you need to make secure requests to retrieve and modify Medidata Platform API resources.

> **Info**
>
> **NOTE:** Write your API integration so as to be resilient to backward compatible changes. For more information, see Medidata Deprecation Policy and Backward Compatibility.

  

square

To access Medidata Platform API resources, you must register an API app with Medidata. After you register your app, start making authenticated HTTP requests to the Medidata Platform API platform. _keypair

# Generate Private-Public Key Pair

You must generate public and private RSA keys to register your app. You supply the public key to Medidata Platform and then use the private key to sign your API requests. The Medidata Platform uses your corresponding public key to authenticate signed requests.

There are numerous methods for generating RWS key pairs.

- Medidata provides a simple command line tool for generating RSA keypairs for use with mAuth. See the Service Authentication with mAuth video for using this tool, as well as information about Medidata's authentication protocol.
- Here is [an online tool](https://cryptotools.net/rsagen) to easily generate an RSA public/private key pair. > **Info** > > **Note:** The public/private key pairs require 2048 characters.
- Use the command line to generate the key paid The Medidata Platform uses your corresponding public key to authenticate signed requests. In the following steps, we describe how to create these keys using the Unix [OpenSLL](https://www.madboa.com/geek/openssl/#introduction) command-line utility. > **Note** > > **Important**: The public/private key pairs require 2048 characters. > > > > Always save your private keys in a secure but accessible place. It is your responsibility to store and safeguard your private key, not Medidata's. > > > > If you lose your private key, you can re-register with a new public key. Access API resources again a few minutes after you make this change. To generate the public/private key pair from a UNIX terminal command line:
   1. Change to the directory where you want to store your RSA private/public keys; for example, the /.ssh directory. > **Info** > > **Note**: The RSA key can be in any directory. Some Medidata client software asks you to declare in a .yml file where the key is; for example, the [Medidata authentication client](https://learn.medidata.com/en-US/bundle/clinical-cloud-api/page/authentication_client_software.html). In the following steps, we use the /.ssh directory. > > > > On the Mac, you can use the Application>Utilities>Terminal program.
   2. To create the RSA keys in the .ssh directory, enter: ```bash
cd ~/.ssh
```
   3. From your Unix terminal emulator, to generate the private key enter ```bash
% openssl genrsa -out key.pem 2048
``` You can name the private .pem key file anything you wish; for example, private_rsa_key.pem.
   4. Press **Return**. You may see information like the following display: ```bash
Generating RSA private key, 2048 bit long modulus
...............+++
................................................................................................+++
e is 65537 (0x10001)
```
   5. To generate the public key, enter ```bash
% openssl rsa -in key.pem -outform PEM -pubout -out public.pem
``` You can name the public .pem key file anything you wish; for example, public_rsa_key.pem
   6. Press **Return**. > **Info** > > **Note:** Your public key will be in the public.pemfile. If you choose to add the private and public keys to unique file names, the pair will be in two files with those names, that is, [unique_private_filename].pem and [unique_public_filename].pem.
   7. Check that the path to the key files is correct. ```bash
% ls ~/.ssh
key.pem
public.pem
```
   8. To send the public key to register your API app as described in Registering Your API App, enter ```bash
% cat ~/.ssh/public.pem
```
   9. Copy the output from your terminal window and paste it into a ZenDesk ticket for your request to register your API app. ```bash
-----BEGIN PUBLIC KEY-----
MIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEAtHVnQk3in9YXe/glI/vl
2eDobdPv2jb6MMQhDLsQHXAYD2AdkoaLUFbnXAhN+ZHPDfhiCkmmwSSjkeLUnfJE
5VLbXXa5+ElIKFu83Hy4bbEoTb2SgSS3qv28LjeXzgBr+6Ux1Cap/Jidczd/QBGV
MasGGYW3TwXdNHoP6/p7DR9A0WaMLyQE+cR4SQxu02MJrDTuLADSKZVbjkMOGx84
dpV300mzcjgh0xvlw+j7KVX886vQ5rpWvMDP6V9sxjPuy30KaxCoBudZ5yVl1AAU
8f5sDRb4RjNIrZ9Wv1UPnJRXAuUr3Eg9LBnVsiOvpFQ7wPL329HPUshNpfyzo3mh
RwIDAQAB
-----END PUBLIC KEY-----
```

# Register Your API App

To connect with Medidata Platform and access API resources, you must register your *API app* with iMedidata. An API app is a trusted application that can make HTTP calls to the Medidata Platform. Registering your app:

- allows it to make authenticated API calls for Medidata Platform resources. _apiUUID
- produces the app uuid. You must include the **APP UUID** in the authentication header when [making authenticated HTTP requests](https://learn.medidata.com/en-US/bundle/clinical-cloud-api/page/your_first_request.html) .

> **Info**
>
> **Note**: You can reregister your API app with Medidata by sending a new public key to the Medidata account representative. This might be required, for example, if your private key is compromised or lost. Again, **never** share your private key with anyone, not even Medidata.

1. Send an email with the following information Send email to [helpdesk@mdsol.com](mailto:helpdesk@mdsol.com) Include the following information **Email Text** I am requesting a new API app for: Using the instructions in the documentation, [generate an SSH public/private key pair](https://learn.medidata.com/en-US/bundle/medidata-platform-api/page/get_started_with_medidata_platform_restful_api_resources.html#GetStartedwithMedidataPlatformRESTfulAPIResources-GeneratePrivate-PublicKeyPair). Add the public key information here: Medidata will send you the new API app name and the app UUID. The Medidata authentication protocol (mAuth) uses the app UUID to authenticate your API requests with the authentication header. **Authorization** Do you need to authorize your API app to access API endpoints? If you require authorization, fill out the information below. What API endpoints do you need authorization for? ([See the API documentation](https://learn.medidata.com/en-US/bundle/medidata-platform-api/page/api_endpoint_quick_reference.html) for lists of resources and endpoints.) From the API documentation, select the resources for which you are selecting API endpoints; for example, Clinical Supplies, Enrollments, Issues and Actions, and so on. Resource you are requesting authorization for: List the entire endpoint URL for which you want authorization; that is, [https://api.mdsol.com/sws/study_environments/{study_environment_uuid}/article_types](https://api.mdsol.com/sws/study_environments/{study_environment_uuid}/article_types) . Endpoint you want to receive authorization for: > **Info** > > **Note:**Work with your Medidata account representative to identify the resources for which you require authorization.
   - **Company Name**:
   - **SSH Public Key**:
   - **API App Name:**
   - **API App UUID:**
   - **Endpoint 1**:
2. The registration process generates a 36-character UUID known as the **app UUID**. Use this UUID in the authentication header when [making authenticated HTTP calls](https://learn.medidata.com/en-US/bundle/clinical-cloud-api/page/your_first_request.html). **You are now ready to make authenticated HTTP calls!**
