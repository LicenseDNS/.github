
# DNS Based Software Licensing Secured with DNSSEC

[LicenseDNS](https://www.LicenseDNS.net/) transforms the way you verify licenses within your software product, streamlining what can often be a complex and tedious process. Traditionally, verifying licenses has required intricate cryptographic methods that often present challenges in implementation and maintenance. However, with LicenseDNS, you can simplify this task significantly by utilizing the robust capabilities of DNS servers. 

Instead of embedding complicated cryptographic algorithms in your application, you simply send a DNS query to a reliable recursive DNS server. This advanced approach enables you to retrieve verified license information quickly and efficiently, with a high level of confidence in its accuracy. As a result, you can shift your focus away from the intricacies of [license verification](https://www.LicenseDNS.net/how-it-works/) and dedicate more of your time and resources to enhancing the core functionalities of your software, ultimately improving the user experience and overall product quality.

LicenseDNS is a powerful solution that enables software vendors to implement [secure licensing mechanisms](https://www.licensedns.net/blog/dns-based-licensing-implementation/) using DNSSEC (Domain Name System Security Extensions). By leveraging this technology, developers can validate licenses effortlessly. To check a license's authenticity, simply send a DNS query to any DNS server, and you will receive license data that has been cryptographically verified for integrity and security. This system is designed to be versatile, supporting all platforms and programming languages, ensuring that vendors can easily integrate it into their existing software solutions.

All programming languages and operating systems, including Android and iOS, are covered. Different programming languages have libraries and functions that make it easier to send queries to Domain Name System (DNS) servers. You can also use some OS commands to send DNS queries, which helps with activating and checking licenses.

See [getting started](https://www.licensedns.net/documents/getting-started/) page.


# Some Details


**LicenseDNS** offers a paradigm shift in software licensing by elegantly offloading the complexities of license verification to the well-established and globally distributed Domain Name System (DNS) infrastructure. Instead of burdening your application with intricate cryptographic routines and the associated overhead of key management and algorithm maintenance, LicenseDNS leverages the inherent scalability and reliability of DNS.

Consider the traditional approach: developers often integrate libraries that handle cryptographic signing and verification, potentially introducing dependencies, increasing the application's footprint, and requiring ongoing attention to security vulnerabilities within these libraries. Furthermore, managing and distributing cryptographic keys securely across numerous deployments can be a significant operational challenge.

LicenseDNS elegantly sidesteps these complexities. When your software needs to verify a license, it constructs a simple DNS query – much like the queries used every day to translate website names into IP addresses. This query is then directed to a standard recursive DNS resolver, the same infrastructure that powers internet browsing. The magic lies in how the license information is encoded within the DNS records and secured using DNSSEC.

**DNSSEC: The Foundation of Trust**

The core of LicenseDNS's security lies in its utilization of DNSSEC (Domain Name System Security Extensions). DNSSEC provides a crucial layer of authentication and integrity to the DNS system. It works by digitally signing DNS records using cryptographic keys. These signatures allow verifying resolvers to confirm that the DNS data they receive has not been tampered with during transit and that it originates from the legitimate authoritative name server for the domain.

**How License Verification Works with LicenseDNS:**

1.  **License Encoding:** When a software license is issued, the relevant information (e.g., license type, expiration date, allowed features, associated user/device identifiers) is encoded into a specific type of DNS record, such as a TXT record, associated with a unique subdomain or hostname.
2.  **DNSSEC Signing:** The authoritative DNS server for the vendor's domain cryptographically signs these DNS records using its private key. The corresponding public key is published in the DNS hierarchy in a special record called a DNSKEY record.
3.  **License Query:** When your software needs to verify a license, it constructs a DNS query for the specific subdomain or hostname associated with that license.
4.  **Recursive Resolution and Validation:** The query is sent to a recursive DNS resolver (often provided by the user's ISP or a public service like Google Public DNS or Cloudflare DNS). This resolver performs the standard DNS resolution process, ultimately reaching the authoritative name server for the vendor's domain. Critically, if DNSSEC is enabled (as it is with LicenseDNS), the resolver will also perform cryptographic validation of the received DNS records using the public key retrieved from the DNSKEY record.
5.  **Verified Response:** The recursive resolver returns the requested DNS record (containing the license information) along with the DNSSEC signatures. Because the resolver has cryptographically verified the authenticity and integrity of this data, your application can trust that the license information is genuine and has not been altered.
6.  **License Interpretation:** Your software then parses the verified license information from the DNS record and acts accordingly, enabling or disabling features based on the license details.

# **Advantages of this Approach**

**1. Simplified Implementation and Reduced Development Overhead:**

-   **Elimination of Complex Cryptography:** The most significant advantage is the removal of the need to implement and maintain intricate cryptographic algorithms (like RSA, ECC, etc.) directly within your software. This drastically simplifies the codebase related to license verification.
-   **Leveraging Existing Infrastructure:** Instead of building custom verification mechanisms, LicenseDNS utilizes the well-established and universally accessible DNS infrastructure. Developers can rely on standard DNS client libraries or operating system commands, reducing the learning curve and development effort.
-   **Reduced Codebase and Dependencies:** By offloading the cryptographic heavy lifting, the size and complexity of your application's licensing module are significantly reduced. This can lead to faster development cycles, easier debugging, and a smaller application footprint.
-   **Focus on Core Functionality:** Developers can dedicate more time and resources to enhancing the core features and user experience of their software, rather than grappling with the intricacies of license management.

**2. Enhanced Security and Trustworthiness:**

-   **Leveraging DNSSEC:** The foundation of LicenseDNS's security is DNSSEC, a robust and widely deployed security extension for DNS. DNSSEC provides cryptographic authentication of DNS data, ensuring that license information retrieved is genuine and hasn't been tampered with. This level of security is often more robust than custom-built cryptographic solutions, which can be vulnerable to implementation errors.
-   **Decentralized Security:**  The security of LicenseDNS is distributed across the DNS infrastructure, benefiting from the collective security efforts and best practices implemented by DNS operators worldwide.
-   **Reduced Risk of Cryptographic Vulnerabilities:**  By relying on the well-vetted DNSSEC standard, you mitigate the risk of introducing vulnerabilities that can arise from implementing custom cryptographic solutions. Security experts continuously analyze and strengthen DNSSEC.
-   **Tamper-Proof License Information:** DNSSEC ensures the integrity of the license data from the authoritative server to the verifying client. Any alteration during transit would be detected by the DNSSEC validation process.

**3. Platform and Language Agnosticism:**

-   **Universal Compatibility:** DNS queries are a fundamental part of internet communication and are supported by every major operating system (Windows, macOS, Linux, Android, iOS) and virtually all programming languages. This makes LicenseDNS inherently cross-platform and language-agnostic.
-   **Easy Integration:** Regardless of your technology stack, integrating LicenseDNS is straightforward. You can utilize built-in DNS resolution functionalities or readily available DNS client libraries in your chosen programming language.
-   **Consistent Verification Mechanism:** The license verification process remains consistent across all supported platforms, simplifying development and support.

**4. Scalability and Reliability:**

-   **Highly Scalable Infrastructure:** The DNS system is designed to handle massive volumes of queries efficiently. LicenseDNS leverages this inherent scalability, ensuring that your license verification process can handle a growing user base without performance bottlenecks.
-   **Globally Distributed and Resilient:** The DNS infrastructure is globally distributed and highly redundant, providing high availability and reliability for license verification, even in the face of network outages.
-   **Caching for Performance:** Recursive DNS resolvers cache DNS records, including license information, which can significantly reduce latency and improve the speed of subsequent license checks.

**5. Centralized License Management and Easier Updates:**

-   **Centralized Control:** License information is managed centrally on the authoritative DNS server. This simplifies the process of updating license details, such as expiration dates or feature entitlements.
-   **Global Propagation:** Changes made to license records on the authoritative DNS server are automatically propagated globally through the DNS system, ensuring that all clients eventually receive the updated information.
-   **Simplified Revocation:** License revocation can be implemented by updating the corresponding DNS record. While propagation times need to be considered, this offers a more straightforward revocation mechanism compared to some traditional methods.

**6. Reduced Application Size and Complexity:**

-   **Smaller Application Footprint:**  By eliminating the need for bulky cryptographic libraries, the overall size of your software application can be reduced, leading to faster downloads and installations.
-   **Simplified Application Architecture:**  The licensing component of your application becomes less complex, making it easier to understand, maintain, and test.

**In conclusion, LicenseDNS presents a compelling alternative to traditional software licensing mechanisms by cleverly harnessing the power and security of the DNS infrastructure. Its simplicity, reliance on established protocols, and broad compatibility make it an attractive option for software vendors looking to streamline their license verification process while maintaining a high level of security and integrity.**

# Working Principle

LicenseDNS operates through a dedicated and customized DNS server that efficiently manages the activation and deactivation processes of software licenses in response to specific DNS queries. The workflow begins when a license is generated via the license manager, at which point it is securely stored in a centralized database.

When a DNS query is received pertaining to the activation or deactivation of a particular license key, the server first performs a comprehensive validation check to ascertain the legitimacy and status of the license. This involves cross-referencing the incoming query with the existing records in the database.

Once validated, the server creates the necessary records that detail either the activation or deactivation process. These records are then digitally signed (DNSSEC) to ensure their integrity and authenticity. Finally, the signed records are returned to the user, confirming the successful activation or deactivation of the requested license key. This systematic approach ensures that all license transactions are handled securely and efficiently, providing users with a seamless experience.

A DNS server processes and responds to DNS queries exclusively when the DNSSEC (Domain Name System Security Extensions) flag is enabled. This mechanism is designed to ensure that only securely signed DNS records are returned to the user, providing an additional layer of security against threats such as spoofing or cache poisoning. By verifying the authenticity and integrity of the DNS data through cryptographic signatures, DNSSEC helps to assure users that the responses they receive are legitimate and have not been tampered with during transit.

The DNS server necessitates a specific format for domain names to effectively process activation and deactivation requests. This format ensures that the server can correctly interpret and manage the commands associated with these requests.

The licensing root domain name is established as q.LicenseDNS.net. It is essential that there are exactly three labels (subdomains) preceding this root domain.

1.  **Request Command:** The first label signifies the request command, which can either be "activate" or "deactivate." For simplification, only the first letters of these commands are utilized—'a' for activate and 'd' for deactivate.
2.  **Hash Value:** The second label consists of the first 32 characters of a hash value generated from the concatenation of the license key and the product ID. This hashing process is crucial as it helps protect the confidentiality of the license key, ensuring that sensitive information is not exposed or easily decipherable.
3.  **Device or User Fingerprint:** The final label is used to bind the license to a specific device or user and can be any string with a length ranging from 1 to a maximum of 32 characters. This fingerprint serves to uniquely identify the device or user associated with the license, reinforcing the security and integrity of the licensing process.

As an example, to activate the license key _12345-12345-12345-12345_ for the product ID _ADA14AE9-08A8-4AE2-B69E-AAE277B8346F_ on a device with a specific generated fingerprint or device ID labeled as _sample-fingerprint_, please follow the detailed steps outlined below.

1.  **Label Assignment for Activation:** The first label you will need to use for activation is designated as 'a.' This label will serve as the primary identifier in the activation process.
2.  **Generating the Hash Value:** To generate the necessary hash value for the activation, you can refer to the sample Java code provided. `DigestUtils.sha256Hex(licenseKey + productId).substring(0, 32);`_ This code performs the following actions:
    1.  It concatenates the license key and the product ID.
    2.  It computes the SHA-256 hash of the concatenated string.
    3.  Finally, it extracts the first 32 characters from the resulting hash. The resulting string will be 7F3735C907D319640373EFA17E196059 when run.
3.  **Formulating the Domain for DNS Queries:** Once you have obtained the hash value from the previous step, the next task is to formulate the domain to which you will send the query. The resulting domain will be structured as follows: `a.7F3735C907D319640373EFA17E196059.example-fingerprint.q.LicenseDNS.net`
4.  **Sending the DNS Query:** You can send the DNS query using various methods depending on your application needs:
    1.  **Programmatically:** You can use different programming languages and libraries to perform DNS queries.
    2.  **Operating System Commands:** If you're using a Linux system, you can utilize command-line tools like _delv_ or _dig_.
    3.  **DNS-over-HTTPS (DoH):** For enhanced privacy and security, you can send a DoH request to public DNS servers like Google (https://dns.google) or Cloudflare (https://1.1.1.1).
5.  **Getting the Result:** If the license key is valid and activation allowed, the following example result will occur. Those TXT values can be used in any way to implement licensing.

  <pre>$ delv a.7F3735C907D319640373EFA17E196059.example- fingerprint.q.licensedns.net -t txt +short +trust
	; fully validated
	"anything"
	"result=success"
	"company=Acme Co."
	"fullname=John Doe"
	"email=john@acme.com"
	"some-key=some-value"
	"feature1=some-value1"
	"feature2=some-value2"
	"epochtime=1742590074543"
	"datetime=2025-03-21 20:47:54"</pre>

Certain TXT records are consistently populated with specific information that is crucial for understanding the context. Among these, the "result" record provides the outcome of a particular operation, while the "epochtime" record captures the time in epoch format, which is essential for time-stamping purposes. Additionally, the "datetime" record presents a human-readable date and time, offering clarity on when the data was generated.

On the other hand, user-specific details such as "fullname," "email," and "company" are included only if they have been specified during the license generation process in the license management system. This means that these details will not appear in the TXT records unless the user has intentionally provided them at the time of license creation, allowing for a more tailored and personalized licensing experience.


[LicenseDNS.net](https://www.LicenseDNS.net/)
