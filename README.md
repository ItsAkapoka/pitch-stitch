# The Pitch Stitch

The Pitch Stitch is an AI-powered elevator pitch generator built for Thread Studio. It guides users through a series of questions about their work, experience, audience, and goals, then uses AI to generate personalized elevator pitches.

🔗 **Live Project:** https://pitch-stitch.santiharbison13.workers.dev

## About the Project

The goal of The Pitch Stitch is to help professionals explain what they do in a way that feels clear, natural, and personal.

Instead of just simply asking users for information and returning a result, the tool creates an interactive experience. It reacts to users' answers, can ask follow-up questions when more detail is needed, and produces multiple versions of an elevator pitch for different situations.

The project is deployed as a real web application and is connected to Thread Studio's existing website.

## Features

- AI-generated personalized elevator pitches
- Seven-question interactive experience
- AI reactions to user responses
- Follow-up questions when answers need more detail
- Multiple pitch formats, including "The Handshake" and "The Room"
- Speech-to-text answer input
- Copy-to-clipboard functionality
- Interactive UI and animated selection buttons
- Responsive design for desktop and mobile
- Error handling and API rate limiting
- Secure API key management

## Technologies Used

- HTML
- CSS
- JavaScript
- Cloudflare Workers
- Anthropic Claude API
- Git & GitHub
- Squarespace

## How It Works

The frontend collects the user's answers through an interactive questionnaire.

The application sends requests to a serverless backend running on Cloudflare Workers. The backend securely communicates with Anthropic's Claude API and returns personalized responses to the frontend.

The Anthropic API key is stored as a Cloudflare runtime secret so it is never exposed in the frontend or repository.

## Development & Debugging

While deploying the project, I encountered an API authentication problem where the application could reach Anthropic but requests returned a 401 authentication error.

Using Cloudflare's production logs, I traced the problem to the application's environment configuration. The API key had been configured as a build variable instead of a runtime secret, which meant the Worker could not access it while processing requests.

After identifying the issue, I moved the API key to Cloudflare's runtime secrets and verified that the application could successfully communicate with the Anthropic API.

This experience gave me hands-on experience debugging a deployed application, working with environment variables, API authentication, serverless infrastructure, and production logs.

## What I Learned

Through this project, I gained experience with:

- Building and deploying a full web application
- Connecting a frontend to a serverless backend
- Working with external APIs
- Handling JSON requests and responses
- Managing API keys and secrets securely
- Debugging production errors using logs
- Working with cloud deployment environments
- Using GitHub for source control and deployment
- Improving UI interactions and user experience
- Integrating a custom application with an existing business website

## Project Structure

`public/index.html` contains the frontend interface and client-side functionality.

`src/index.js` contains the Cloudflare Worker backend, API routes, AI prompts, error handling, and Anthropic API integration.

`wrangler.jsonc` contains the Cloudflare Worker configuration.

`package.json` contains the project's package information and deployment script.

## Status

The Pitch Stitch is deployed and functional. Future updates may include additional UI improvements, analytics, custom domain integration, and improvements based on user feedback.
