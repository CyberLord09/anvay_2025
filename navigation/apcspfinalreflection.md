---
layout: post 
search_exclude: true
show_reading_time: false
permalink: /cspfinalblog
title: AP CSP Final Blog
comments: true
---

{% include nav/blogs.html %}

# CrossWise Trimester Reflection

This trimester, working on **CrossWise** was a major step forward in both my technical growth and understanding of real-world software development. Our goal was to create a platform that predicts border wait times, displays live feeds, provides historical footage, and visualizes data in meaningful ways. Every part of the stack—from backend APIs to frontend dashboards—was built by our team using real tools, real data, and real deployment.

## 🧠 Skills I Developed

| **Skill** | **What I Learned** | **What I Built** |
|----------|--------------------|------------------|
| **Full-Stack Development** | Working across both frontend and backend | Built features across Flask APIs and the Jekyll/JS frontend |
| **Flask & REST APIs** | Creating and securing API endpoints with JSON responses | Routes for video metadata, weather data, map overlays, and JWT login |
| **Google Maps API** | Integrating external APIs for route and mapping tools | Added border route planning with predicted wait-time overlays |
| **MoviePy & Video Processing** | Automating video clipping and organization | Script to generate 3x daily time-sliced clips stored by timestamp |
| **Data Handling** | Processing JSON, CSV, and external API payloads | Merged CBP wait data with historical weather info for analysis |
| **Chart.js** | Creating interactive data visualizations in the browser | Live graph of traffic/weather synced with video and map layers |
| **Authentication** | Using JWT, sessions, and facial login methods | Built secure login with role-based access and auto logout logic |
| **Frontend Design (HTML/CSS/JS)** | Crafting responsive interfaces with Tailwind & JavaScript | Built the calendar UI, timelapse viewer, and live dashboard |
| **Git & GitHub Collaboration** | Branching, pull requests, conflict resolution | Worked on feature branches, managed commits, opened/closed issues |
| **Deployment** | Hosting frontend and backend separately | Static frontend on GitHub Pages; Flask backend on Railway or EC2 |

---

## 🛠️ Features I Helped Build

### 🎥 Timelapse and Live Video System
- Wrote the logic to pull and store border camera video clips throughout the day.
- Integrated historical playback via a clickable calendar interface.

### Calender UI Updates
 - Updated the calender to work seemless with the page

---

## 🌱 Personal Reflection

Before this trimester, I had experience with Python and basic web development—but this project pushed me into real-world full-stack work. I had to think about:
- **API security**
- **data structures**
- **frontend UX**
- **deployment automation**
- and **team-based collaboration.**

Debugging backend errors and seeing them fixed on the frontend gave me a deeper appreciation for how web apps work at every level. More than just learning syntax, I learned **how to build something that works**, how to communicate in code, and how to handle unexpected problems like service outages, merging conflicts, or user-side issues.

---
---
---

Working on CrossWise this trimester has been one of the most challenging and rewarding technical experiences I’ve had so far. When I joined the team, I knew we were trying to solve a real-world problem—predicting border wait times and making the travel experience smoother—but I didn’t yet realize how deep and multifaceted the work would be.

At the start, I focused on understanding the core problem and backend structure. I helped implement and test APIs built with Flask that connected different parts of the system—from fetching live traffic camera feeds to storing historical data for prediction. Along the way, I learned how to design endpoints that are clean, secure, and scalable. I got comfortable working with REST principles, route structuring, and passing JSON payloads back and forth between the client and server.

Beyond just the API layer, I also worked on integrating time-based video storage. Our goal was to automatically capture and store video clips from border crossing cameras at three different points during the day—morning, midday, and night—then organize them by date. This involved building out backend logic using MoviePy and cron-like scheduling to automate the clipping, as well as designing file structures to keep things maintainable. Debugging and refining this system taught me a lot about file I/O, memory usage, and error handling in production-like environments.

On the frontend, I helped develop the traffic history dashboard, which allows users to explore archived clips through a calendar-based interface. This required close coordination between HTML templates, JavaScript interactions, and API calls. I had to think about user experience, layout clarity, and responsiveness. Every element—from the video preview to the "Now Playing" label—had to work smoothly and update dynamically.

Later in the trimester, I worked on one of my favorite features: the border directions tool. I helped integrate the Google Maps API with our custom wait-time predictor so that users could receive accurate driving directions and see our model’s predicted delays. This involved intercepting travel time estimates, applying our prediction model output, and reflecting those changes visually on the map. To make this work, I had to understand both mapping APIs and how to layer on our ML estimates in a way that didn’t confuse or overwhelm the user.

One of the biggest lessons I’ve learned from this project is how to think like a developer building for real people. We weren’t just coding to complete an assignment—we were coding to create a product. That meant thinking about design, accessibility, error messages, edge cases, and even things like what happens when a video feed goes offline. I learned to work across the stack and to jump between frontend code, Flask logic, and shell scripts with confidence.

Perhaps just as important, I learned how to work on a team. We had to share responsibilities, review each other’s code, solve merge conflicts, and give constructive feedback. I also gained a lot of experience writing commits with clear messages, handling version control in GitHub, and staying organized across issues and milestones.

CrossWise wasn’t just a technical challenge—it was a crash course in project management, real-world collaboration, and learning by doing. I’m proud of how much we built in a single trimester, and even more excited about what we can continue to improve. This experience has made me a better developer, a better teammate, and someone who’s even more excited to build technology that solves real problems.