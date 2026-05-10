---
title: Petabytes of Internet Archive Data at the Tip of Your Fingers
summary: If you know the bucket name that is 😄
date: 2026-05-06T09:00:00-04:00
authors:
  - name: diegoripley
    link: https://github.com/diegoripley
    image: https://github.com/diegoripley.png
tags:
  - internet-archive
  - ia
excludeSearch: false
draft: true
---

We have added the `internetarchive` bucket to [https://s3.labs.dataforcanada.org](https://s3.labs.dataforcanada.org), which proxies directly to the Internet Archive. This opens up a massive amount of data to standard S3 API calls, but there are a few important caveats regarding performance and discovery.

```mermaid
flowchart TD
    Client(["🌐 S3 Client / User"])
    Gateway["<b>s3.dataforcanada.org</b>\nS3-Compatible Gateway"]

    Client -->|"S3 API Request"| Gateway

    Gateway -->|"sourcecooperative bucket"| AWS
    Gateway -->|"backblaze-ca-east-006 bucket"| BB
    Gateway -->|"cloudflare-apac bucket"| CFAPAC
    Gateway -->|"cloudflare-enam bucket"| CFENAM
    Gateway -->|"internetarchive bucket"| INTERNETARCHIVE
    Gateway -->|"tigris bucket"| TIGRIS

    subgraph AWS ["☁️ Amazon Web Services"]
        AWSNode["📍 Oregon, United States"]
    end

    subgraph BB ["🔵 Backblaze B2"]
        BBNode["📍 Toronto, ON, Canada"]
    end

    subgraph CFAPAC ["🟠 Cloudflare R2"]
        CFAPACNode["📍 Asia Pacific Region"]
    end

    subgraph CFENAM ["🟠 Cloudflare R2"]
        CFENAMNode["📍 Eastern North America"]
    end

    subgraph INTERNETARCHIVE ["📚 Internet Archive Data"]
        INTERNETARCHIVENode["🗃️ San Francisco, United States and Vancouver, Canada"]
    end

    subgraph TIGRIS ["⚡ Tigris Data"]
        TIGRISNode["11 Regions Worldwide 🌍\nAuto-routes to nearest location\nfor lowest latency"]
    end

    style Gateway fill:#1a5f7a,color:#fff,stroke:#0d3d52
    style Client fill:#2d6a4f,color:#fff,stroke:#1b4332
    style AWSNode fill:#ff9900,color:#000,stroke:#cc7a00
    style BBNode fill:#e03c31,color:#fff,stroke:#b02d24
    style CFAPACNode fill:#f6821f,color:#fff,stroke:#c4681a
    style CFENAMNode fill:#f6821f,color:#fff,stroke:#c4681a
    style TIGRISNode fill:#6c3483,color:#fff,stroke:#512e6b
    style INTERNETARCHIVENode fill:#000,color:#fff,stroke:#512e6b
```

## The Quest for Efficiency

Integrating the Internet Archive wasn't without its hurdles. I started by using the official Internet Archive endpoint defined in their [ias3 documentation](https://archive.org/developers/ias3.html) (https://s3.us.archive.org). Unfortunately, even when using authenticated API keys, requests were throttled almost immediately.

![landscape](2026-05-06_10-42-ia-slowdown.png)

To make this architecture **as efficient as possible**, I had to pivot. Instead of relying on the standard S3 endpoint, I switched the backend to utilize the Internet Archive's native HTTP paths, wrapping them in a custom S3 interface:

* `http://archive.org/download/{identifier}` for optimized file downloading.
* `https://archive.org/metadata/{identifier}` for fetching JSON metadata.

Even with this highly optimized, custom approach, you will still encounter rate throttling. We have added a bandwidth quota of **30GB per 5 minutes**.

## How to Access the Data

Because of how this proxy functions, you currently need to know the exact identifier (which acts as your bucket) of the dataset you want to access.

Let's use the `earth-at-night-2016` dataset as an example. Behind the scenes, the native archive links look like this:

* **Download:** https://archive.org/download/earth-at-night-2016
* **Metadata:** https://archive.org/metadata/earth-at-night-2016

Through our gateway, you can access this identical dataset using standard S3 protocols simply by pointing your client here:

* **S3 Gateway:** https://s3.labs.dataforcanada.org/internetarchive/earth-at-night-2016
![Internet Archive listing dataset](internet-archive-listing-s3.png)

## What's Next?

Right now, finding these dataset identifiers requires manually browsing the Internet Archive. Because this proxy implementation is now as fast and efficient as the upstream rate limits will allow, my next goal is to improve discovery.

In the future, I plan to build a simple, searchable file and metadata index of the Internet Archive directly into the platform. I'm a big fan of movies, so I'll be starting the indexing process there!