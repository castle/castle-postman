# github.com/castle/castle-postman

This repository contains a Postman Collection to use for interactions with the Castle API.

To use this collection, you need an active Castle API key. [Sign up for a free Castle account here](https://dashboard.castle.io/signup/new).

# Quick Start
1. Import `Castle.postman_collection.json` to your Postman Workspace
2. Import `Castle-Sandbox.postman_environment.json` to your Postman Environments (this declares a single environment variable, `api_secret`)
3. Set the `api_secret` environment variable to the API key for your Castle environment (found in your Castle Dashboard Settings - we recommend the "Sandbox" environment)
4. Send requests! Start with a request from the **Send Login Endpoint Events** Folder

# Try Castle with Real-World Scenarios for a Login Endpoint

Are you looking for a way to explore real-world scenarios with a Castle integration? We have a few play-by-play scenarios that show how Castle can help protect a user account via integration at the login endpoint.

Check out our [Scenarios](./Scenarios.md) page for details.

Castle can integrate with many endpoints. Additionally, you can customize the behavior of Castle to meet business or security requirements for individual endpoints and user scenarios.

# Collection Organization

The requests in this collection are organized into a few folders:
- [Send Login Endpoint Events](#send-login-endpoint-events)
  - [with Random Data](#with-random-data)
  - [with Persistent Data](#with-persistent-data)
  - [with Mostly-Persistent Data](#with-mostly-persistent-data)
    - [and a Random IP](#and-a-random-ip)
    - [and a Random User-Agent](#and-a-random-user-agent)
    - [and a Random IP and User-Agent](#and-a-random-ip-and-user-agent)
    - [and a Random User](#and-a-random-user)
- [Device Management](#device-management)
- [User Impersonation (Ignore Events)](#user-impersonation-ignore-events)
- [User Management](#user-management)

### A Note on Using Custom Variables

>All requests in the collection use "collection variables" which are purposely obfuscated for ease-of-use. Pre-request scripts and tests are used to modify these variables with precise intent, based on the folder name and hierarchy.
>
>If you desire to set your own custom values for requests, you may create environment variables of the same name as the variable you're trying to overwrite. This allows you to delete or clear those custom environment variables in order to restore the "default" behavior of this collection.

## Send Login Endpoint Events

- This folder constructs `$login.succeeded` and `$login.failed` events with randomized or persistent data, and sends those events to Castle. The requests in this folder are organized into sub-folders based on whether randomized or persistent data is used.

> with Random Data
>
>-  Send events using **randomly generated data for all user and device characteristics**. This randomly-generated data is generated via pre-request scripts, and saved in the collection variables.
>
> with Persistent Data
>
>- Send events using **data fetched from the collection variables**.
>
> with Mostly-Persistent Data
>
>- Send events using *mostly* data that is fetched from the collection variables, but with one or two things randomly generated:
>>
>> and a Random IP
>>
>>- Send events using a random IP, but otherwise persistent data (same user & device).
>>
>> and a Random User-Agent
>>
>>- Send events using a random User-Agent, but otherwise persistent data (same user & IP).
>>
>> and a Random IP and User-Agent
>>
>>- Send events using a random IP and User-Agent, but otherwise persistent data (same user).
>>
>> and a Random User
>> 
>> - Send events using random user details, but otherwise persistent data (same device info).

## Device Management

- This folder contains requests to Castle's [Device Management Endpoints](https://docs.castle.io/device_management_tool/). These endpoints are designed to be used for admin-level management of end-user devices (i.e. for an internal dashboard). Some of them can be integrated with authenticated application endpoints to allow users to self-manage their own devices.

## User Impersonation (Ignore Events)

- This folder contains requests that demonstrate Castle's [Impersonation Mode Capabilities](https://docs.castle.io/impersonation_mode/). The `/impersonate` endpoint is used to tell Castle that a user is being impersonated (i.e. by an admin or support personnel) and therefore Castle should ignore the events originating from the device that is actively impersonating the user.

## User Management

- This folder contains requests to Castle's [User Data Management Endpoints](https://docs.castle.io/gdpr_apis/). These are used for deleting users or for retrieving all information about a user that Castle has stored.