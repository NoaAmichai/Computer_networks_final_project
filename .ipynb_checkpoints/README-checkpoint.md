# Computer networks final project

Introduction:

Secure messaging applications like WhatsApp and Telegram have become common for personal and group communications. These apps provide end-to-end encryption to protect message contents from prying eyes. However, some metadata such as who is talking to whom and when is still potentially vulnerable to surveillance through traffic analysis.

This project explores whether traffic patterns alone can reveal insights into a user's group memberships and messaging habits, even when the messages themselves are encrypted. Prior academic work has shown some success in attributing encrypted traffic to destination services and contacts by analyzing traffic timing, size patterns, and more. We aim to recreate and expand on some of these techniques through a practical messaging app traffic analysis.

Our Approach <br>
We focused our analysis on WhatsApp due to its popularity and encrypted protocol. Actual WhatsApp Web traffic from multiple test groups was captured using Wireshark packet sniffing. This traffic was then processed using custom Python scripts to extract attributes like inter-message timing and message sizes.

Visualizations of these traffic patterns were generated for each group. We looked for unique characteristics in the timing and size graphs that could serve as fingerprints to identify a specific group. Beyond simple visualization, we implemented algorithms from an academic paper on traffic analysis attacks on messaging apps. These techniques attempt to correlate timing and size patterns across users to deduce group membership.

Our experiments tested scenarios where the target user is a member of only a single group at a time, as well as more complex cases with multiple simultaneous group memberships. In our analysis, we explore whether these fingerprinting and correlation-based attacks prove successful at deducing group information in both settings.

The full methodology, results, and discussion are documented in the project report (report.pdf). The Python analysis scripts, sample captures, and output graphs are also provided in this repository.


To execute the code, follow these steps:
1. Begin by cloning the repository to your local machine.
2. Navigate to the "src" folder within the cloned repository.
3. Inside the "src" folder, locate the notebook you want to run.
4. Open the notebook using your preferred Jupyter Notebook environment.
5. Once the notebook is open, you can execute its cells to run the code and generate results.
6. The generated graphs and images will be stored in the "res" folder.
By following these steps, you'll be able to easily run the code, visualize the outcomes, and access the graphs and images produced during the execution of the notebook.


Contents
* src: Contains the source code for traffic capturing, analysis.
* resources: Contains sample pcap files of messaging app traffic.
* results: Output graphs, and other result files from traffic analysis and attacks.
* report.pdf: Project report with answers to the dry part questions.
  

Cleaning Process<br>
The raw packet capture contains many extraneous packets unrelated to the WhatsApp web traffic we aim to analyze. To isolate the relevant WhatsApp packets, we filter the data as a preprocessing step.

Specifically, we filter the packets to only keep those with TCP port 443. This port is used for HTTPS encrypted traffic. Since WhatsApp communications are encrypted between the client and WhatsApp's servers, the WhatsApp web packets are transmitted over port 443.
By removing the extraneous non-443 packets, we are left with a clean subset of the traffic that contains only the WhatsApp web communications we intend to study. This filtered data can then be analyzed to extract information specifically about the WhatsApp usage without interference from unrelated packets.

After filtering the packets by port 443, we applied an additional filter to only keep packets with the TLS protocol. TLS (Transport Layer Security) is used to encrypt the actual WhatsApp payload data.
The raw capture contains other TCP packets like ACKs, push requests, etc that are part of the TCP handshake and transmission but do not contain the WhatsApp messaging content. By further filtering down to just TLS packets, we isolated the encrypted WhatsApp data being sent and received.
This two-step filtering approach of first selecting port 443 and then choosing TLS packets gives us only the TLS-encrypted WhatsApp data, removing all other extraneous packets. This filtered subset contains the core information we want to analyze regarding the WhatsApp web session.

After filtering by port and protocol, we filtered the packets further based on the source and destination IP addresses.
To get the server IP, we used nslookup on the WhatsApp web domain. This gave us the IP address of the WhatsApp server we were communicating with.
For the client IP, we used ifconfig on our machine to get our local IP address.
Using these two IP addresses, we filtered the packet capture to only keep packets going between our computer and the WhatsApp server. This removed any other extraneous traffic in the capture.

At this point, the filtered dataset contains only the WhatsApp web packets sent between our client and the server. However, there may still be some noise from other WhatsApp groups being captured.
Overall, the multi-stage filtering process resulted in a clean subset of packets relevant to our analysis. By removing unnecessary packets, we are left with only the WhatsApp web traffic to study further.
Now that preprocessing is complete, we can move on to analyzing the timing, size patterns, and other characteristics of this filtered WhatsApp packet data.

Insights




References
* GitHub/Computer_networks_final_project/project-paper.pdf

Submitted by
* Avi Ostroff
* Noa Amichai 
