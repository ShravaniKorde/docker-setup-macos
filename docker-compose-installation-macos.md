Docker Compose Setup on macOS 11🐳

Steps:

Check Docker Engine works:

docker version

OR docker --version


Download Docker Compose v2.20.2 (recommended for Docker 24.x and macOS 11):

mkdir -p ~/.docker/cli-plugins

curl -SL https://github.com/docker/compose/releases/download/v2.20.2/docker-compose-darwin-x86_64 \
-o ~/.docker/cli-plugins/docker-compose

chmod +x ~/.docker/cli-plugins/docker-compose

Test it:

docker compose version

You should see something like: Docker Compose version v2.20.2

## 🐋 Create and Run a Test Project
### Create a Directory & docker-compose.yml

mkdir hello-docker
cd hello-docker
nano docker-compose.yml


Paste the following into docker-compose.yml:
version: "3.9"
services:
web:
image: nginx:alpine
ports:
- "8080:80"



Click ctrl O and then enter. Click ctrl x.

### Run the Container
docker compose up -d



And then open this link to access the nginx container at:
👉



















But if you encounter any error like this:

error pulling image configuration: download failed after attempts=6: ...
lookup docker-images-prod...cloudflarestorage.com: no such host



### 1. Check Internet Connection
Make sure your Mac has a working internet connection and can resolve public domains.
Try in Terminal:
ping
If this fails — fix your network connection first.
What it should look like -




### 2. Test DNS Resolution
Check if your system can resolve Docker's image host:
nslookup
nslookup

If your DNS is working correctly for docker.io and cloudflare.com, then this is not a general DNS issue. The error you're facing is more specific to how Docker is trying to resolve or reach a CDN-backed subdomain (used by Docker Hub to serve image layers).
To resolve, try manually resolving the failing host. This is a deeper check.
In terminal:

nslookup docker-images-prod.6aa30f8b08e16409b46e0173d6de2f56.r2.cloudflarestorage.com

If it fails with “no such host” — then the DNS server you’re using (2409:...) does not resolve this dynamic Cloudflare R2 subdomain.

It may look like this:

If DNS is failing, try switching to a public DNS like Google DNS or Cloudflare DNS:
To do this:
Open System Preferences > Network > Advanced > DNS
Add:
1.1.1.1
8.8.8.8
Click OK then Apply.
Then in terminal try again
docker compose up -d
You should now see like this:


And then open this link to access the nginx container at:
👉


### Success!🎉
Your Docker Compose is now set up and working perfectly on macOS 11.
You can now use it to manage multi-container applications with ease. Happy Dockering! 🐳

FYI:
Docker Compose binary is stored at  ~/.docker/cli-plugins/docker-compose

