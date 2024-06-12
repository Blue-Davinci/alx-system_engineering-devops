Postmortem: Aggregate RSS Feed Aggregator Outage

Issue Summary:

Duration: The outage lasted from 14:00 to 16:30 EAT on June 11, 2024.
Impact: The Aggregate RSS feed service was down, resulting in a complete service disruption. Users experienced timeouts and server errors when attempting to access feeds. Approximately 75% of users were affected.
Root Cause: A misconfiguration in the server.js file caused an infinite loop, leading to memory exhaustion.
Timeline:

14:05 EAT - Issue detected by automated monitoring alert.
14:10 EAT - Initial assumption was a DDoS attack; network traffic was analyzed.
14:25 EAT - Engineer noticed unusually high memory usage on the server.
14:45 EAT - Investigation revealed no signs of DDoS; focus shifted to server configuration.
15:00 EAT - Misleading path: Checked for database issues; none found.
15:30 EAT - Incident escalated to the backend team.
16:00 EAT - Root cause identified in server.js file.
16:30 EAT - Service restored after fixing the server.js configuration.
Root Cause and Resolution:

Cause: An update to the server.js file introduced a code snippet that lacked proper exit conditions, causing an infinite loop.
Resolution: The code was corrected to include exit conditions, and the server was rebooted to clear the memory exhaustion.
Corrective and Preventative Measures:

Improvements: Implementing stricter code review processes and enhancing monitoring to detect memory anomalies.
Tasks:
Review and merge pull requests only after thorough testing.
Patch server.js to prevent future infinite loops.
Add memory usage alerts to monitoring systems.
Conduct a workshop on best practices for server configuration.
This postmortem outlines the events and actions taken during the Aggregate service outage, providing a clear path to preventing similar incidents in the future.
