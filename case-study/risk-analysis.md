# Risk Analysis

The assessment identified several exposed services that are expected within an internal enterprise environment but still represent elevated risk if improperly secured.

Key services included SSH for remote administration, PostgreSQL for database access, and multiple Splunk management and ingestion interfaces. These services are considered high-value targets due to their potential impact on system integrity, data confidentiality, and monitoring capabilities if compromised.

OS fingerprinting produced multiple candidate matches, highlighting a realistic challenge in security monitoring where operating system identification is not always definitive. This ambiguity reinforces the importance of correlating multiple data points — such as service banners, TCP/IP behavior, and port responses — before drawing conclusions.

UDP scan results returned limited visibility, with one port identified as open or filtered. This behavior is consistent with real-world environments where UDP services are often restricted or obscured by firewall rules. No evidence of unauthorized or unnecessary UDP services was observed.

No critical vulnerabilities were identified during the vulnerability scan phase. Automated findings were manually reviewed to eliminate false positives, underscoring the importance of analyst validation rather than relying solely on tool output.
