###  Project 1: Building and host a static website for a restaurant + Present AWS Migration benefits.

### Overview
Create a static website for a restaurant experiencing operational challenges. The restaurant is having a high volume of customer bookings, and current system cannot keep up, orders are being mixed up and/or misplaced. The owner wants to use a static website to streamline customer interactions and improve booking/order management. Additionally, prepaRe a presentation on the benefits of migrating to AWS.

!NOTE: This was a group project and the collaborators have been tagged at the bottom of the page.

### Objectives
- Build a static website
- Host the website on an Amazon S3
- Presentation on the benefits of AWS Migration

### Steps taken
### Build Static Website
- Build a website → make it user friendly with clean and minimal design
- Make sure it meets the requirements and needs of the client.
<img width="670" height="645" alt="image" src="https://github.com/user-attachments/assets/27f34c1e-aed2-445d-8ae5-ea9f5dd6cb50" />

### Host Website on S3
prepare the website files

- Create a local folder for files → `html`, `css` and `assets`
- Create bucket
- In console: search S3 → create bucket → choose a unique name

<img width="1366" height="556" alt="image" src="https://github.com/user-attachments/assets/7bb11e47-1bcf-435c-9338-5311ec896e60" />

### Turn on static website hosting
In console management: `open bucket` → `go to properties` → `static website hosting` →`enable` → `choose Host a static website` →` set index document` → `save.`

<img width="1366" height="586" alt="image" src="https://github.com/user-attachments/assets/47028d6c-b276-4778-909f-70f2d94b08dc" />

### Allow public read

- S3 has public access blocked by deafault, so its best to use a bucket policy that allowspublic access

- Disable Block Public Access for the bucket `(Permissions → Block public access → Edit → uncheck relevant settings and confirm)`

<img width="1366" height="581" alt="image" src="https://github.com/user-attachments/assets/db15af1c-2ba9-4b39-9b56-5aef96fccbe3" />

### Upload files and test website

Console managent : `Open the bucket → Upload → Add files/folders → Upload.`

- Once hosting enabled and files uploaded,
-  open the bucket website endpoint → `find the exact endpoint URL in the bucket Properties → Static website hosting.`
-   If index loads, hosting is successful.
<img width="1366" height="553" alt="image" src="https://github.com/user-attachments/assets/8fa21586-211d-48ba-b1bf-096f9dc65f50" />

### Overall learning experience
### Challenges

- Public access- the struggle was with why the site was not opening and showing a "forbidden" message, blocked public access and figuring which JSON policy to use.
- HTTPS/HTTP confusion- the challenge was that browser on https blocks the site and the site is considered to be not secure.
File structure and case sensitivity- the challenge was that Images were not loading, and being inaware of case-sensitivity (Index.html istead of index.html).

### Wins
- Practical understanding of cloud storage concepts- how objects are stored. -- How bucket URLs work and the differences between normal and cloud storage.
- Learning about IAM and access controls- gained experienced on bucket policies, difference between public and private access, building confidence with AWS permissions.
Hands-on experience with static site architecture- clears understanding on what static hosting means, and the lack of a server, improving knowledge of how websites actually work.

### Presentation
<img width="1401" height="785" alt="image" src="https://github.com/user-attachments/assets/6d2db37e-f289-4afd-8260-38d05d98c3de" />

- There was also, a presentation on benefits of migrating to aws and restaurant overview. This presentation shows the ways in which Migrating to AWS services offers organizations a modern, scalable, and cost-efficient environment for running applications and data workloads. The process typically involves assessing existing systems, choosing the right AWS tools, and then moving resources into cloud services. Overall, migration enables businesses to modernize their infrastructure, reduce operational overhead, and take advantage of AWS’s global reliability and innovation.
For a full walkthrough and visual breakdown, see presentation:

<img width="1401" height="785" alt="image" src="https://github.com/user-attachments/assets/31a68d6e-d052-42a3-b823-76e595a91e8a" />

### Conclusion
- Completing a project that involves hosting a static website on Amazon S3 provides valuable, hands-on experience with real cloud infrastructure. Through this process, a solid understanding of how AWS storage services operate was gained, including bucket creation, object management, and website configuration. Tere was also a lesson on how to control access using bucket policies and public access settings, and how these security principles apply to real-world deployments. This project reinforces practical cloud skills. It also demonstrates how scalable, low-cost, serverless solutions like S3 can replace traditional web servers. Overall, this project builds foundational knowledge in cloud architecture, strengthens AWS proficiency.

🤝 Collaborators
- UnathiTshoni: https://github.com/tshoniunathi
- Olivia Mahuluhulu: https://github.com/Aluwani-tec/AWS-re-start-journey
- Amogelang Menwe : https://github.com/amogelangmenwe-ops
- Madimetja Galane: https://github.com/Galanemcg/Galanemcg-Madimetja-Galane-AWS-re-Start-Journey
