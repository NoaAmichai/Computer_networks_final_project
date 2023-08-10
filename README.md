# Computer networks final project

Secure messaging applications like WhatsApp and Telegram have become common for personal and group communications. These apps provide end-to-end encryption to protect message contents from prying eyes. However, some metadata such as who is talking to whom and when is still potentially vulnerable to surveillance through traffic analysis.

This project explores whether traffic patterns alone can reveal insights into a user's group memberships and messaging habits, even when the messages themselves are encrypted. Prior academic work has shown some success in attributing encrypted traffic to destination services and contacts by analyzing traffic timing, size patterns, and more. We aim to recreate and expand on some of these techniques through a practical messaging app traffic analysis.

Our Approach
We focused our analysis on WhatsApp due to its popularity and encrypted protocol. Actual WhatsApp Web traffic from multiple test groups was captured using Wireshark packet sniffing. This traffic was then processed using custom Python scripts to extract attributes like inter-message timing and message sizes.

Visualizations of these traffic patterns were generated for each group. We looked for unique characteristics in the timing and size graphs that could serve as fingerprints to identify a specific group. Beyond simple visualization, we implemented algorithms from an academic paper on traffic analysis attacks on messaging apps. These techniques attempt to correlate timing and size patterns across users to deduce group membership.

Our experiments tested scenarios where the target user is a member of only a single group at a time, as well as more complex cases with multiple simultaneous group memberships. In our analysis, we explore whether these fingerprinting and correlation-based attacks prove successful at deducing group information in both settings.

The full methodology, results, and discussion are documented in the project report (report.pdf). The Python analysis scripts, sample captures, and output graphs are also provided in this repository.

Contents
* src: Contains the source code for traffic capturing, analysis.
* resources: Contains sample pcap files of messaging app traffic.
* results: Output logs, graphs, and other result files from traffic analysis and attacks.
* report.pdf: Project report with answers to the dry part questions.

