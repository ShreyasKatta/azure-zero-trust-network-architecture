# 🛡️ Zero-Trust Network Architecture: The ”Invisible Frontend”

<div align="center">
    <img src="https://img.shields.io/badge/Microsoft_Azure-Cloud_Platform-0078D4?style=plastic&logo=microsoftazure&logoColor=white" alt="Azure" />
    <img src="https://img.shields.io/badge/Azure_VPN_Gateway-P2S_Connectivity-0078D4?style=plastic&logo=microsoftazure&logoColor=white" alt="VPN" />
    <img src="https://img.shields.io/badge/Private_Endpoint-Zero_Trust_Network-5C2D91?style=plastic&logo=microsoftazure&logoColor=white" alt="Private Endpoint" />
    <img src="https://img.shields.io/badge/Network_Security_Group-Traffic_Control-FF6F00?style=plastic&logo=microsoftazure&logoColor=white" alt="NSG" />
    <img src="https://img.shields.io/badge/Azure_App_Service-Private_Access-0089D6?style=plastic&logo=microsoftazure&logoColor=white" alt="App Service" />
    <img src="https://img.shields.io/badge/Private_Resolver-Hybrid_DNS-00B294?style=plastic&logo=microsoftazure&logoColor=white" alt="DNS Resolver" />
    <img src="https://img.shields.io/badge/Security-Zero_Trust_Model-8E44AD?style=plastic&logo=shield&logoColor=white" alt="Security" />
</div>

<hr />

<blockquote>
    <strong>Mission Objective:</strong> Completely eliminate the public internet attack surface for sensitive cloud applications. This architecture ensures that the application is <strong>physically unreachable</strong> from the public web, granting access exclusively through an identity-verified secure tunnel.
</blockquote>

<hr />

<h2>🚀 The Core Proof: The "Airlock" Transition</h2>
<p>
    The primary success metric of this project is the binary state of accessibility. Without the secure tunnel, the application does not exist to the outside world.
</p>

<table width="100%">
    <tr>
        <th width="50%" bgcolor="#f8d7da"><font color="#721c24">🔴 State: Public (VPN OFF)</font></th>
        <th width="50%" bgcolor="#d4edda"><font color="#155724">🟢 State: Private (VPN ON)</font></th>
    </tr>
    <tr>
        <td valign="top">
            <ul>
                <li><strong>Action:</strong> Attempting to browse the application URL from the public internet.</li>
                <li><strong>Result:</strong> ❌ <strong>Access Denied.</strong></li>
                <li><strong>Behavior:</strong> The browser returns a <code>403 Forbidden</code> or <code>DNS_PROBE_FINISHED_NXDOMAIN</code>. The application is hidden behind a platform-level lockdown.</li>
            </ul>
        </td>
        <td valign="top">
            <ul>
                <li><strong>Action:</strong> Authenticating via <strong>Entra ID (MFA)</strong> and establishing the VPN tunnel.</li>
                <li><strong>Result:</strong> ✅ <strong>Access Granted.</strong></li>
                <li><strong>Behavior:</strong> The <strong>NRPT rules</strong> intercept the request, resolving the URL to a private 10-dot IP address. The internal dashboard loads instantly.</li>
            </ul>
        </td>
    </tr>
</table>

<hr />

<h2>🌌 The Concept: "Security Through Invisibility"</h2>
<p>
    Standard cloud security relies on firewalls to protect public targets. This <strong>Invisible Frontend</strong> architecture moves the target into a subterranean vault where there is no door on the street.
</p>

<h3>🧠 The "Invisible Speakeasy" Analogy</h3>
<ol>
    <li>🚫 <strong>The Street View:</strong> To any passerby, there is no sign and no entrance. If they "knock" (DNS query), they get no answer because the public "phonebook" has no record of the address.</li>
    <li>🛂 <strong>The Secret Handshake:</strong> To enter, you must prove your identity to a guard (<strong>Microsoft Entra ID</strong>). Only after MFA verification are you allowed into the private tunnel (<strong>VPN Gateway</strong>).</li>
    <li>🗺️ <strong>The Secret Map:</strong> Once inside, you receive a special map (<strong>NRPT Rules</strong>). This map reveals the secret location hidden behind a hidden wall (<strong>Private Endpoint</strong>).</li>
</ol>

<hr />

<h2>🏗️ Architecture & Workflow</h2>
<p>
    <strong>The Secure Routing Flow:</strong> <code>Public Internet</code> ➡️ <code>Entra ID Auth (MFA)</code> ➡️ <code>Azure VPN Gateway</code> ➡️ <code>Private DNS Resolver (NRPT)</code> ➡️ <code>Private Endpoint</code> ➡️ <code>App Service</code>
</p>

<ul>
    <li><strong>Platform Lockdown:</strong> All public ingress is disabled at the App Service level. The attack surface is effectively zero.</li>
    <li><strong>Private Link Backbone:</strong> Application traffic is projected into the VNet, ensuring data remains on the Microsoft global backbone.</li>
    <li><strong>Hybrid Name Resolution:</strong> A <strong>Private DNS Resolver</strong> acts as the internal authority, translating public names to private IPs for authorized users.</li>
</ul>

<hr />

<h2>🛠️ The Technical "Flex": NRPT & DNS Interception</h2>
<p>
    The most advanced feature is the manual configuration of the <strong>Name Resolution Policy Table (NRPT)</strong>. This ensures that only specific cloud traffic is routed to the Private Resolver, allowing the user to maintain their normal internet connection while securely accessing internal resources.
</p>

<h3>Custom NRPT Configuration Snippet</h3>
<pre><code>&lt;clientconfig&gt;
  &lt;dnsservers&gt;
    &lt;dnsserver&gt;10.0.1.4&lt;/dnsserver&gt; &lt;!-- Private Resolver Inbound IP --&gt;
  &lt;/dnsservers&gt;
  &lt;dnssuffixes&gt;
    &lt;dnssuffix&gt;.azurewebsites.net&lt;/dnssuffix&gt;
  &lt;/dnssuffixes&gt;
&lt;/clientconfig&gt;</code></pre>

<hr />

<h2>📝 Key Engineering Insights</h2>
<ul>
    <li><strong>DNS Visibility:</strong> Demonstrated that the domain name is a "dead end" to anyone outside the VPN, preventing DNS record leakage.</li>
    <li><strong>Network Hardening:</strong> Successfully transitioned a PaaS service from "Public-First" to "Private-Only" without breaking availability.</li>
    <li><strong>Identity-Centric Access:</strong> Verified that identity, not just location, is the new perimeter in a Zero-Trust world.</li>
</ul>

<hr />

<h2>🎥 Project Walkthrough</h2>
<p align="center">
    <li>Click the image below to watch a live demonstration of the Zero-Trust architecture ⬇️</li>
    <br>
    <a href="https://youtu.be/hjUHxLR26AU" target="_blank">
    <em><img width="1300" height="600" alt="Zero-Trust Network Architecture Thumbnail" src="https://github.com/user-attachments/assets/4e4ee8e6-92a0-4997-8d59-85b27ca9b798" /></em>
    </a>
</p>

<hr />

<p align="center">
    <strong>Project by Shreyas</strong><br>
    <em>Cloud Security Architect</em>
</p>

</body>
</html>
