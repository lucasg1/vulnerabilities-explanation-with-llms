This is the dataset of a work accepted in the 17th International Conference on Agents and Artificial Intelligence (ICAART 2025). The article title is: "A study on vulnerability explanation using Large Language Models".

The filtered ReposVul dataset is available in the reposvul_filtered.json file, with 170 vulnerability test cases. The other files are the outputs from all the models used in the study: CodeLlama (7B, 13B, 34B, and 70B), CodeGeeX4, Gemma 2 27B, and GPT-4o.

An example of a vulnerability explanation is shown below.

Vulnerability: CWE-400 Uncontrolled Resource Consumption ([CVE-2022-24839](https://nvd.nist.gov/vuln/detail/CVE-2022-24839)).

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

Some results comparing GPT-4o with the evaluated models are presented here, other results and graphs can be seen on the [results](results/) folder.

![metric-BLEU](https://github.com/user-attachments/assets/9d6f9597-c19c-46b5-bbd4-64818aa1a3f4)
![metric-ROUGE-L](https://github.com/user-attachments/assets/600a59f2-ece3-4b54-90df-440cd8875799)
![metric-BERT-F1](https://github.com/user-attachments/assets/2ca0a84d-8e1c-434a-bb35-5f5bd8ec6fa2)
![metric-ROUGE-1](https://github.com/user-attachments/assets/cb222a53-e693-4210-b1be-a733f55803e9)
![metric-ROUGE-2](https://github.com/user-attachments/assets/fb9552e7-3550-4a5b-960c-897cf4021fd9)




