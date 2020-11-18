# Want to See Castle in Action? Try These Scenarios
Below are a few event sequences that will allow you to see Castle's real-time risk analysis at work. In these request scenarios, Castle is protecting an application login endpoint. 

- [Profiling User Behavior with Multiple Devices and Multiple IP's](#profiling-user-behavior-with-multiple-devices-and-multiple-ips)
- [Credential Stuffing - Block Malicious Logins](#credential-stuffing-block-malicious-logins)

Note that results may vary slightly because of limitations with Postman's built-in randomizing capabilities. Random IP's, for example, may include private IP ranges. The library is still very useful for exploring the Castle API behavior.

---

## Profiling User Behavior with Multiple Devices and Multiple IP's

Use the sequences below to replicate common user behavior such as switching devices or switching IP addresses. Castle takes into consideration many risk factors, including the geographical distance from the last login, whether the device is part of a network of attacking devices, and whether the device fingerprint is recognized.

1. Establish a random user and random device characteristics 

> Send Login Endpoint Events
>
>> with Random Data (use sparingly)
>>
>>> POST /authenticate $login.succeeded (*send a single request*)

2. Send another login request with that user's credentials from a random IP, with the same device 

> Send Login Endpoint Events
>
>> with Mostly-Persistent-Data 
>>
>>> and a Random IP
>>> 
>>>> POST /authenticate $login.succeeded (*send a single request*)

3. Send another login request with that user's credentials from a random IP, with different random device characteristics 

> Send Login Endpoint Events
>
>> with Mostly-Persistent-Data 
>>
>>> and a Random IP and User-Agent 
>>> 
>>>> POST /authenticate $login.succeeded (*send a single request*)

---

## Credential Stuffing: Block Malicious Logins

Use the sequence described below to replicate a credential stuffing attack. Credential Stuffing attacks commonly have a less-than-1% success rate, but we'll give ours a 3% success rate (33-to-1 failed-to-successful login ratio).

1. Establish the attacking device characteristics

> Send Login Endpoint Events
>
>> with Random Data (use sparingly)
>>
>>> POST /track $login.failed (*send a single request*)

2. Send 33 `$login.failed` events, targeting random user accounts

> Send Login Endpoint Events
>
>> with Mostly-Persistent-Data
>>
>>> and a Random User
>>>
>>>> POST /track $login.failed (*send 33 requests*)

3. Send a `$login.succeeded` event, targeting a random user account

> Send Login Endpoint Events
>
>> with Mostly-Persistent-Data
>>
>>> and a Random User
>>>
>>>> POST /authenticate $login.succeeded (*send a single request*)