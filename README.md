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
- Multiple pitch formats, including "The Handshake" and "The Room"
- Helpful hints that guide users toward stronger, more specific answers
- Structured AI responses for more reliable pitch generation
- Automatic retry if pitch generation encounters an API error
- Speech-to-text answer input
- Copy-to-clipboard functionality
- Interactive UI and animated selection buttons
- Responsive design for desktop and mobile
- Error handling and API rate limiting
- Secure API key management
- Embedded directly into the Thread Studio Squarespace website
- Automatic iframe resizing to match the tool's content
- Automatic scrolling to the top of the tool between questions
- Review screen for viewing all answers before regenerating a pitch
- Ability to edit individual answers without restarting the questionnaire
- Regenerate pitches using updated answers
- Start-over option that safely clears the current session after confirmation

## Technologies Used

- HTML
- CSS
- JavaScript
- Cloudflare Workers
- Anthropic Claude API
- Git & GitHub
- Squarespace

## How It Works

The frontend guides users through seven questions about their audience, work, experience, and goals. Several questions include hints that help users give more specific answers.

As users move through the experience, the application sends requests to a serverless backend running on Cloudflare Workers. The backend securely communicates with Anthropic's Claude API to generate short reactions and the final personalized pitch.

Claude returns structured data with predefined fields instead of plain-text JSON. This makes responses more reliable when generated pitches contain quotation marks, line breaks, or other formatting that could otherwise cause parsing errors.

The final generation step also automatically retries once if an API request fails before displaying an error to the user.

The Anthropic API key is stored as a Cloudflare runtime secret so it is never exposed in the frontend or repository.

The application is embedded into the Thread Studio Squarespace website. When embedded, Pitch Stitch communicates with the parent Squarespace page using browser `postMessage` events.

A `ResizeObserver` detects changes to the application's height and tells the parent page to resize the embedded frame. This allows longer screens, including the final results, to expand naturally without creating a second scrollbar inside the tool.

The application can also notify the parent page when users move to a new question so the page can scroll back to the top of the Pitch Stitch experience.

After receiving their results, users can review all of their original answers in one place. They can edit an individual response, save the change, and return to the review screen without repeating the entire questionnaire.

Users can then regenerate their pitch using the updated answers. They can also choose to start over, which asks for confirmation before clearing the current answers and returning to the welcome screen.

## Development & Debugging

While deploying the project, I encountered an API authentication problem where the application could reach Anthropic but requests returned a 401 authentication error.

Using Cloudflare's production logs, I traced the problem to the application's environment configuration. The API key had been configured as a build variable instead of a runtime secret, which meant the Worker could not access it while processing requests.

After identifying the issue, I moved the API key to Cloudflare's runtime secrets and verified that the application could successfully communicate with the Anthropic API.

This experience gave me hands-on experience debugging a deployed application, working with environment variables, API authentication, serverless infrastructure, and production logs.

Later in development, I encountered another production issue where Claude successfully generated a pitch, but the application sometimes failed while parsing the response as JSON. Generated text could contain quotation marks or line breaks that made plain-text JSON unreliable.

I updated the Anthropic integration to use structured tool responses with predefined schemas for both reactions and final pitches. I also added an automatic retry to the final pitch generation process so a temporary failure gets another attempt before reaching the user.

I also simplified the user flow by removing AI-generated follow-up questions and adding contextual hints beneath key questions instead. This keeps users moving forward while still encouraging more detailed answers.

## What I Learned

Through this project, I gained experience with:

- Building and deploying a full web application
- Connecting a frontend to a serverless backend
- Working with external AI APIs
- Handling structured API requests and responses
- Designing schemas for reliable AI-generated data
- Managing API keys and secrets securely
- Debugging production errors using logs
- Handling failures and implementing retry logic
- Working with cloud deployment environments
- Using GitHub for source control and deployment
- Improving UI interactions and user experience
- Designing user guidance without interrupting the main flow
- Integrating a custom application with an existing business website
- Communicating between an iframe and its parent page with `postMessage`
- Using `ResizeObserver` to respond to dynamic layout changes
- Integrating and dynamically resizing a web application inside Squarespace
- Managing application state across multiple screens
- Building an edit-and-review workflow without restarting the application
- Reusing existing question components for different user flows
- Safely resetting application state
- Designing confirmation steps for destructive user actions

## Project Structure

`public/index.html` contains the frontend interface and client-side functionality.

`src/index.js` contains the Cloudflare Worker backend, API routes, AI prompts, error handling, and Anthropic API integration.

`wrangler.jsonc` contains the Cloudflare Worker configuration.

`package.json` contains the project's package information and deployment script.

## Status

The Pitch Stitch is deployed and functional as a live tool for Thread Studio and is integrated directly into the company's Squarespace website.

Recent updates improved production reliability and user experience through structured AI responses, automatic retry handling, contextual answer hints, simplified question flow, dynamic embedded resizing, answer review and editing, pitch regeneration, and session reset controls.

The application continues to be improved through testing, debugging, and feedback from real-world use.

## Recent Updates

### September 2026

- Added structured Anthropic responses to prevent JSON parsing failures
- Added automatic retry handling for pitch generation
- Removed follow-up questions to create a smoother question flow
- Added contextual hints to help users write stronger answers
- Added dynamic resizing and scrolling for the Squarespace embed
- Added a review screen for viewing and editing previous answers
- Added pitch regeneration after editing answers
- Added a confirmed "Start over" option that resets the session
