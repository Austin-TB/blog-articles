# How I Host My Personal Fullstack Projects (for Basically $0/month)

So, I’ve been building a few small personal projects lately, mostly stuff to play around with and show off in my portfolio.

And while deploying them, I realized: I don’t need AWS-sized infra or $30/month managed services just to host a to-do app no one’s using yet.

After a bunch of experimenting, here’s the setup I landed on: cheap, actually free, simple, and good enough to make my projects look real without breaking my wallet.

---

## The Setup

Here’s the overall idea:

- **Frontend:** Deployed on **Vercel (Hobby plan)**
- **Backend:** Hosted on **Google Cloud Run**
- **Docker images:** Built locally, pushed to **Docker Hub**
- **Cost:** $0 unless I forget to delete something

This combo gives me a clean deployment pipeline, nice URLs, HTTPS, and all the fancy cloud stuff without needing to worry about scaling, uptime, or CI/CD pipelines.

---

## 1. Frontend on Vercel

This part’s really easy.

If you’ve got a React, Next.js, or Svelte app, Vercel basically does all the magic for you.

1. Push your frontend to GitHub.
2. Go to [vercel.com](https://vercel.com/).
3. Click **“New Project”**, connect your repo.
4. Let it auto-detect the framework.
5. Deploy.

Done. You’ll get a URL like `myshittyapp.vercel.app`.

I use this for literally all my projects now. It’s fast, free, and the DX is smooth.

---

## 2. Backend on Google Cloud Run

Now for the backend.

I usually write small FastAPI servers, just enough to have an API endpoint that looks legit.

The main trick: you can deploy **directly from Docker Hub** to Cloud Run and avoid Cloud Build charges entirely.

### Here’s the process I use:

1. Build and push your Docker image:
    
    ```bash
    docker build -t myusername/mybackend:latest .
    docker push myusername/mybackend:latest
    
    ```
    
2. Go to the Google Cloud Console → **Cloud Run → Create Service**
3. Under “Deployment platform,” choose:
    
    ```
    Deploy one revision from an existing container image
    
    ```
    
4. Enter your image path:
    
    ```
    docker.io/myusername/myapi:latest
    
    ```
    
5. In the **Autoscaling** section, set:
    
    ```
    Maximum number of instances: 1
    
    ```
    
    That’s your budget protection. Keeps Google from spinning up 50 containers when no one’s using your app.
    
6. Allow **unauthenticated invocations** (unless you like 403s).
7. Click **Deploy** and grab your service URL.

You’ll get something like:

```
https://mybackend-xyz123.a.run.app

```

---

## 3. Connect Frontend + Backend

Now back in your frontend, just point your API calls to that Cloud Run URL.

Example `.env`:

```
VITE_API_BASE_URL=https://myapi-xyz123.a.run.app

```

Then rebuild and redeploy your frontend on Vercel. Done.

(Also: don’t forget CORS if your API is public. I lost 20 mins debugging that once.)

---

## 4. Add a Budget in Google Cloud

Even though Cloud Run’s free tier is generous, it’s smart to set a budget, especially if you tinker a lot.

Go to:

```
Billing → Budgets & alerts → Create budget

```

Set something tiny like `$5`. That way, if something loops or scales unexpectedly, you’ll get an email before your card cries.

---

## 5. Sanity Tips

A few random notes from my personal chaos:

- Make sure your backend listens on **port 8080** (Cloud Run needs that).
- You can test your container locally before pushing:
    
    ```bash
    docker run -p 8080:8080 myusername/myapi
    
    ```
    
- Keep max instances = 1 unless you actually have users.
- Cloud Run free tier gives you 2M requests per month, plenty for demo apps.
- Don’t bother setting up Cloud Build unless you love waiting and paying.

---

## 6. That’s It

And that’s pretty much the whole setup.

It’s simple, free, and perfect for hosting:

- Small portfolio projects
- Demo APIs
- Personal tools or dashboards
- Anything that looks serious but doesn’t actually need to scale

My current monthly cost: **$0.00**

My stress level: **also near zero**

If you’re just showing off your work or trying to learn deployment pipelines, this stack (Vercel + Cloud Run + Docker Hub) is honestly one of the easiest and cheapest ways to go live.

---
