# Highly Available AWS VPC Architecture with Public EC2 and Private RDS

<h3 class="" data-start="263" data-end="289"><strong data-start="267" data-end="289">Objective:</strong></h3>
<p class="" data-start="290" data-end="398">To demonstrate the ability to design and deploy a secure, highly available AWS infrastructure consisting of:</p>

<ul data-start="399" data-end="656">
 	<li class="" data-start="399" data-end="487">
<p class="" data-start="401" data-end="487">A custom VPC with public and private subnets across multiple Availability Zones (AZs),</p>
</li>
 	<li class="" data-start="488" data-end="540">
<p class="" data-start="490" data-end="540">An internet-facing EC2 instance in public subnets,</p>
</li>
 	<li class="" data-start="541" data-end="585">
<p class="" data-start="543" data-end="585">A private RDS instance in private subnets,</p>
</li>
 	<li class="" data-start="586" data-end="656">
<p class="" data-start="588" data-end="656">All within the AWS Free Tier, with no impact on credit card charges.</p>
</li>
</ul>
<h3 class="" data-start="663" data-end="693"><strong data-start="667" data-end="693">Tools &amp; Services Used:</strong></h3>
<ul data-start="694" data-end="1027">
 	<li class="" data-start="694" data-end="703">
<p class="" data-start="696" data-end="703">AWS VPC</p>
</li>
 	<li class="" data-start="704" data-end="732">
<p class="" data-start="706" data-end="732">Subnets (Public &amp; Private)</p>
</li>
 	<li class="" data-start="733" data-end="751">
<p class="" data-start="735" data-end="751">Internet Gateway</p>
</li>
 	<li class="" data-start="752" data-end="766">
<p class="" data-start="754" data-end="766">Route Tables</p>
</li>
 	<li class="" data-start="767" data-end="811">
<p class="" data-start="769" data-end="811">EC2 (Amazon Linux 2023 Free Tier instance)</p>
</li>
 	<li class="" data-start="812" data-end="868">
<p class="" data-start="814" data-end="868">RDS (Free Tier-eligible DB, e.g., MySQL or PostgreSQL)</p>
</li>
 	<li class="" data-start="869" data-end="886">
<p class="" data-start="871" data-end="886">Security Groups</p>
</li>
</ul>
<img class="alignnone size-full wp-image-82" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/awsachi.png" alt="" width="741" height="781" />
<h3>Step-by-Step Deployment Process:</h3>
<h4>1. AWS Account Setup</h4>
<ul>
 	<li>Created a new AWS Free Tier account</li>
</ul>
<h3>2. VPC and Networking Setup</h3>
<ul>
 	<li>Created a custom VPC (10.0.0.0/16).</li>
</ul>
<img class="alignnone wp-image-83 size-medium" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-238-300x267.png" alt="" width="300" height="267" /><img class="alignnone wp-image-84 size-large" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-239-1024x351.png" alt="" width="640" height="219" />


<h3></h3>
<h3>Created 4 subnets:</h3>
<ul>
 	<li>2 Public Subnets in different AZs (10.0.1.0/24 and 10.0.2.0/24)</li>
 	<li>2 Private Subnets in different AZs (10.0.3.0/24 and 10.0.4.0/24)</li>
</ul>
<img class="alignnone size-full wp-image-86" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-245.png" alt="" width="1344" height="528" />

I enabled <strong>Auto-assign Public IP</strong> on public subnets.

<img class="alignnone wp-image-87 size-large" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-247-1024x160.png" alt="" width="640" height="100" />


<ul>
 	<li>I created and attached an <strong>Internet Gateway (IGW)</strong> to the <strong>VPC</strong>.</li>
</ul>
<img class="alignnone wp-image-88 size-large" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-249-1024x229.png" alt="" width="640" height="143" />

<img class="alignnone wp-image-89 size-large" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-250-1024x302.png" alt="" width="640" height="189" />
<h3>I created Route Tables:</h3>
<ul>
 	<li>Public RT: Route to IGW.</li>
</ul>
<img class="alignnone wp-image-90 size-large" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-252-1024x479.png" alt="" width="640" height="299" />

I associated the two <strong>Public Subnets (1&amp;2)</strong> to the <strong>Public Route Table</strong>

<img class="alignnone wp-image-91 size-full" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-254.png" alt="" width="854" height="510" />


I also created a <strong>Private Route Table</strong> for the private subnets and I associated the two <strong>Private Subnets (1&amp;2)</strong> to the <strong>Private Route Table</strong>

<img class="alignnone wp-image-92 size-full" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-255.png" alt="" width="817" height="483" />
<h3>3. EC2 Instance Deployment</h3>
<ul>
 	<li>I launched a <strong>t2.micro EC2 instance</strong> (Amazon Linux 2023) in one of the public subnets.</li>
</ul>
<img class="alignnone size-full wp-image-93" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-257.png" alt="" width="1364" height="195" />

I launched another a <strong>t2.micro EC2 instance</strong> in another public subnet in another availability zone

<img class="alignnone size-full wp-image-95" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-259.png" alt="" width="1371" height="360" />

<h3>4. RDS Deployment</h3>
<ul>
 	<li>Launched a Free Tier-eligible RDS instance (MySQL/PostgreSQL) in one of the private subnets.</li>
 	<li>I disabled public accessibility.</li>
 	<li>I created a DB subnet group using the private subnets.</li>
 	<li>I created a Security Group for RDS:</li>
 	<li>I allowed inbound traffic only from EC2's private IP/security group.</li>
</ul>
<img class="alignnone size-full wp-image-96" src="https://eyemekacyberportfolio.name.ng/wp-content/uploads/2025/04/Screenshot-261.png" alt="" width="1323" height="327" />
<h2>Conclusion</h2>
<p class="" data-start="3610" data-end="3650">This project demonstrates my ability to:</p>

<ul data-start="3651" data-end="3847">
 	<li class="" data-start="3651" data-end="3698">
<p class="" data-start="3653" data-end="3698">Design a secure, multi-AZ architecture on AWS</p>
</li>
 	<li class="" data-start="3699" data-end="3745">
<p class="" data-start="3701" data-end="3745">Isolate backend databases from public access</p>
</li>
</ul>
