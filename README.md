This is the dataset of a work accepted in the 17th International Conference on Agents and Artificial Intelligence (ICAART 2025). The article title is: "A study on vulnerability explanation using Large Language Models".

The filtered ReposVul dataset is available in the reposvul_filtered.json file, with 170 vulnerability test cases. The other files are the outputs from all the models used in the study: CodeLlama (7B, 13B, 34B, and 70B), CodeGeeX4, Gemma 2 27B, and GPT-4o.

An example of a vulnerability explanation is shown below.

Vulnerability: CWE-400 Uncontrolled Resource Consumption (CVE-2022-24839)

```java
protected void scanPI() throws IOException {
    if (c == '?' || c == '/') {
        char c0 = (char)c;
        c = fCurrentEntity.read();
        if (c == '>') { // Vulnerability: no check for end-of-stream
            break;
        }
        fStringBuffer.append(c0);
    }
}
```

Explanation by models GPT-4o and CodeLlama 34B.

```json
% GPT-4o explanation
{
    "why": "The vulnerability occurs because the loop continues reading and appending characters without proper limit checks or conditions, potentially leading to excessive resource consumption.",
    "danger": "Exploiting this vulnerability could lead to denial of service by consuming excessive memory or CPU resources, rendering the application unresponsive or unavailable to legitimate users.",
    "how": "An attacker could exploit this by sending input that keeps the loop running indefinitely, consuming all available resources until the system becomes unresponsive.",
    "fix": "To fix this vulnerability, implement proper bounds checking or limiting mechanisms to ensure that resources are not consumed excessively when appending characters to the buffer."
}
% CodeLlama 34B explanation
{
    "why": "The vulnerability happens because the code does not properly control the allocation and maintenance of a limited resource, which can lead to the exhaustion of available resources.",
    "danger": "The danger of this vulnerability is that an attacker can exploit it to consume all available resources, leading to a denial of service (DoS) attack.",
    "how": "The vulnerability can be exploited by sending a large number of requests to the server, each request containing a large number of characters that are not properly handled by the code, leading to an increase in resource consumption.",
    "fix": "To fix this vulnerability, the code should be modified to properly control the allocation and maintenance of resources, such as by limiting the number of requests that can be made in a given time period, or by implementing a rate limiting mechanism to prevent excessive resource consumption."
}
```


